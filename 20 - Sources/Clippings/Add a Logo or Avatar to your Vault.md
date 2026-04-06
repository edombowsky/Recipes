---
title: "Add a Logo or Avatar to your Vault"
source: "https://tfthacker.com/experiment-vault-logo"
author:
published:
created: 2025.07.05 00:00:00.000 -0700
description: "Dashboard++ — a simple organization and navigation method for Obsidian Vaults - Toolbox for Thought"
tags: ["clippings"]
obsidianUIMode: "preview"
modified: Saturday, July 5th 2025, 4:41:16 pm
updated: 2025.11.16 00:06:20.019 -0800
---
In the summer of 2024, I released one of my new tools, [JournalCraft for Obsidian](https://tfthacker.com/jco). This vault teaches good journaling and includes several templates. As I developed it, I wanted to give it a unique appearance that would help it stand out visually. One of the things I did was put a logo in the upper left-hand corner.

![vault-logo-jcc.png](https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/Experiments/media/add-vault-logo/vault-logo-jcc.png)

This logo gives [JournalCraft for Obsidian](https://tfthacker.com/jco) a unique look compared to other vaults.

Several individuals have written to me asking me how I did this. After receiving several requests, I saw that this is another way people could customize their vaults, such as by adding a logo, avatar, or profile picture. For example, someone might want to decorate their vault with a family photo:

![vault-logo-dpp.png](https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/Experiments/media/add-vault-logo/vault-logo-dpp.png)

This solution is simple if you know CSS, but it might be a bit more advanced if you don't. I will walk you through the process step-by-step.

## Step-by-step Instructions

### Download the Sample Vault

I'd recommend downloading my sample [Dashboard++](https://github.com/TfTHacker/DashboardPlusPlus) vault, which includes a working implementation of the technique I will document here. The previous image illustrates what this vault looks like.

This will allow you to see the working solution and use it for comparison as you work on your vault.

Let us get started with work in your vault. Please open your vault in Obsidian.

![mail.jpg](https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/media/homepage/mail.jpg)

promo-embed-newsletter

### Add a Folder to Your Vault

In your vault, create a folder called `0-Vault-Logo`. This folder serves a particular purpose. In the next step, we will add a CSS Snippet. That CSS snippet looks for a folder in the vault called `0-Vault-Logo` and replaces the folder name with an image.

Don't worry; this folder will not be visible in Obsidian, as it serves as a placeholder for the logo.

### Add the vault-logo.css Snippet

Create a file named vault-logo.css in the./obsidian/snippets folder in your vault. If you are unfamiliar with CSS Snippets, you can learn more about this feature from the Obsidian online documentation: [CSS snippets - Obsidian Help](https://help.obsidian.md/Extending+Obsidian/CSS+snippets).

In the `vault-logo.css` file, add the text found in the CSS snippet from this link: [vault-logo.css snippet on GitHub](https://github.com/TfTHacker/DashboardPlusPlus/blob/master/.obsidian/snippets/vault-logo.css). This link brings you to this web page:

![vault-logogithub-raw-copy.png](https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/Experiments/media/add-vault-logo/vault-logogithub-raw-copy.png)

You can click the copy text button, as the red arrow indicates in this image, to quickly grab all the text from the CSS snippet.

Paste that text into the file `vault-logo.css` in your vault.

#### Enable the CSS Snippet in Obsidian

In Obsidian, go into **Settings**.

1. Select the **Appearance** tab.
2. Then scroll down to the **CSS Snippets** section and click the **refresh snippets** button.
3. Finally, toggle on the `vault-logo.css` button.

![vault-logo-enable-snippet.png](https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/Experiments/media/add-vault-logo/vault-logo-enable-snippet.png)

Now close the Settings window in Obsidian, and if all has gone well, you should see the following logo in your vault:

![vault-logo-closeup-logo.png](https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/Experiments/media/add-vault-logo/vault-logo-closeup-logo.png)

Of course, we now have one problem: this is not an image of your family. The next step is to provide the image you want to display as a logo.

#### Providing an Image for the Logo

I wish this next step were more straightforward, but it isn't. Since we use a CSS Snippet, Obsidian limits us to the types of images we can display.

One supported way to display an image in a CSS snippet in Obsidian is to display an image from the internet. However, this defeats the purpose of Obsidian being an offline tool.

A second supported way to display an image in CSS is to use a base64-encoded image, which we will do.

What is a base64-encoded image?

A base64-encoded image is like turning a picture into a string of letters and numbers. It's a way to hide the picture inside a long code so you can send it easily in a message or a webpage. Simply put, it converts an image into a string of text that represents the image. We can use this base64 text in the CSS Snippet.

#### Convert an Image to Base64

Using a free online tool, such as the [Base64 Image Encoder](https://elmah.io/tools/base64-image-encoder/), you can take an image from your computer and have this tool generate the base64 text we need for our CSS Snippet.

<video controls="" src="https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/Experiments/media/add-vault-logo/vault-log-convert-to-base64.mp4#t=0.001"></video>

This tool takes the image and creates the base64 text.

#### Replace the Base64 Image in the CSS Snippet

Now, let us return to the CSS Snippet `vault-logo.css` you created earlier in your vault.

This is the tricky part, requiring the precision of a surgeon. You must replace the existing base64 image text in the CSS snippet with the new base64 image text you created in the previous step.

In the following clip, you can see how this is done.

<video controls="" src="https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/Experiments/media/add-vault-logo/vault-log-replacing-base64.mp4#t=0.001"></video>

Notice that the existing base64 text is selected and removed. Then, we pasted and saved the new base64 image text into the file. Don't hesitate to pause the video to see what is happening in more detail.

You will also notice the base64 text is VERY long!!!

If all goes well, you should see your logo in the upper left-hand corner of the window. This is what my logo looks like now in Obsidian:

![vault-logo-tfthacker-logo.png](https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/Experiments/media/add-vault-logo/vault-logo-tfthacker-logo.png)

## Using This in Your Vault or Theme

#### Credits

Please feel free to use this technique in your solutions, such as themes or vaults for the community. If you do so, please credit this article and include a link to it.

![01-promo1.jpg](https://publish-01.obsidian.md/access/5482717c61d4cd4a5e39468efa73a612/_pub/media/store/journal-craft/01-promo1.jpg)

promo-embed-home
