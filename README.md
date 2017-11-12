![EmbedJouranl](https://embedjournal.com/assets/images/logo/embedjournal-120px.png)

EmbedJournal.com Contents
=========================

This repository has raw contents of embedjournal.com. Blog posts are written in the familiar [GitHub Flavored Markdown (GFM)](https://github.github.com/gfm/).

If you are planning on writing a blog post to be placed on EmbedJournal.com, you are in the right place, read on. We also suggest you have a look at our [guest blogging policies](https://embedjournal.com/guest-blogging/) if you haven't done so already.

## Dependencies

This repository depends on [Perl](https://www.perl.org/) and [imagemagic](https://github.com/ImageMagick/ImageMagick). If you are on a Linux machine, you most probably already have Perl. You will have to install imagemagic from your distro's repository. If you are on debian based system, you can do,

```sh
apt install imagemagic
```

## Creating a new post

The contents of this repository are part of a bigger build process and hence require proper formatting to create a successful build. We have written some scripts to automate this process and help reduce errors.

### Working with drafts

First you start off by creating a draft. You can do that with the help of `mkpost` script at the top level of the repository.

```sh
$ ./mkpost --draft
```

The above command will ask for various information for the first time you run it. Fill them all out and you will find the draft created in `drafts/` directory. Inside the `drafts/draft-*/` directory that was created just now, you will find a `post.md` file where you are write your post.

### Adding images to your post

All relevant images files are to be added in your drafts directory. We suggest you resize the image to some reasonable dimension and geometry. Larger images cause performance hit on the destination web page.

Once you have an image `image-name.jpg` in the same directory as post.md, you can add the following line in your `post.md` where you would like to insert that image.

```liquid
[ image src="image-name.jpg" ]
```

You could also add optional alt tag or caption to your images like so,

```liquid
[ image src="image-name.jpg" alt="Image Name" caption="My image caption" ]
```

### Adding a thumbnail for your post

An image named `post-thumb.jpg` of resolution 165x165 is acceptable as thumbnail for a post. You can create a thumbnail from an existing image with the help of the `mkpost` script.

```sh
$ ./mkpost --thumb path/to/your-image.png
```

The output of the above script is a 165x165 jpg file called `post-thumb.jpg` is created in the same directory as `your-image.png`. So the ideal work-flow is to place your thumbnail source inside your drafts directory like any other image and execute `mkpost` script and remove the source image soon after.

### Checking your draft

Once you think you are done with your post, you can copy past the contents of `post.md` into the [EmbedJournal editor](https://embedjournal.com/editor/) to check for markdown syntax errors and see how your post will look on production environment (with the exception of images).

After that, you will have to run your draft by our validation script as below,

```sh
$ ./mkpost --verify drafts/draft-your-post-title/
```

Try fixing any errors that are reported by the validation methods.

### Publishing your post

Once you have successfully validated the draft, you have two options for getting the post published.

#### 1. Fork and raise a pull request

Fork this repository and update your git remote URL (if you cloned from this link). After that you can do the following to move your post from `drafts/` directory and merge it into posts directory.

```sh
$ ./mkpost --publish drafts/draft-your-post-title/
```

The images are also moved to the corresponding directory in `images/`. You can review those changes and commit and raise a pull request to this repository.

#### 2. Pack and send in email for review

The other (not preferred) method is to wrap your draft like below

```sh
$ ./mkpost --wrap drafts/draft-your-post-title/
```

Attach the post to an Email and send an email to admin@embedjournal.com copying siddharth@embedjournal.com. We will make the commit for you.
