# FAQ Vencord Edition

<img src="https://media.discordapp.net/stickers/1039992459209490513.png" alt="wq is loading"/>

### Before starting
<p>
Before going or reading further, make sure that you have
installed <format color="red">C H I L L A X </format>
follwoing the instructions given in
<a href="Installation-guide.md">Installation Guide</a> for Vencord.
</p>

### 1. How to change the background/background image of CHILLAX?

The steps are first `settings`, then go to the `VENCORD` Section and then `Themes`.
Finally, click `Edit Quick CSS` which should open integrated
[Monaco](https://microsoft.github.io/monaco-editor/) (*It's already there no need
for installation as this is part of the Vencord itself*) code editor.
Now using this Editor, you can easily edit css with hot reloading.
See the below-attached screenshots:

1. <img src="go_to_settings.png" alt="whatever" border-effect="rounded"/>

2. <img src="edit_quick_css.png" alt="whatever" border-effect="rounded"/>

3. <img src="monaco_editor.png" alt="whatever" border-effect="rounded"/>

Now to go to line number `46` (*at the time of writing, the line number
is 46 which in a later version might change*) or where the variable `--wallpaper`
defined and change the url that is within the single quote `''`
to the **wallpaper**/**gif** **cdn url** that you want to set.

> After opening the `Edit Quick CSS` it's all blank?
> Please check out the detailed installation instructions on
> how to install C H I L L A X the recommended way.
> {style="tip"}

See the below screenshots:

<img src="bg_change.png" alt="whatever" border-effect="rounded"/>

Now your favourite background image/gif should be applied.

> **Note**: If you are using discord CDN, they expire after some time.
> For this the background may suddenly become black or it might start
> blinking or shaking.
> In such cases fetch a new link or download the image and host it
> somewhere like GitHub.

{style="note"}


### 2. How to change/use another font(s)?

First, make sure that the font you are trying to
use is already hosted somewhere if it's not already.
Most of the time you will be using [google fonts](https://fonts.google.com/).
From there, choose the font you are looking for and adjust all the settings
and everything (font weights, size, etc.) and then copy the css import url.
See the below screenshots:

1. <img src="font_change_1.png" alt="wq is loading" border-effect="rounded"/>

2. <img src="font_change_2.png" alt="wq is loading" border-effect="rounded"/>

3. <img src="font_change_3.png" alt="wq is loading" border-effect="rounded"/>

4. <img src="font_change_4.png" alt="wq is loading" border-effect="rounded"/>

5. <img src="font_change_5.png" alt="wq is loading" border-effect="rounded"/>

6. <img src="font_change_6.png" alt="wq is loading" border-effect="rounded"/>
    * Only copy the highlighted part.
      In your case, the link is maybe different.
7. <img src="font_change_7.png" alt="wq is loading"/>
    * Now go to `Settings` > `Themes` > `Edit Quick CSS`.
    * Paste the copied link at the top just like the above screenshot and put the `;` at the end of it.
8. <img src="font_change_8.png" alt="wq is loading"/>
    * Now change the `--font-nane` to the name of the font that you have
      just imported.
    * Optionally adjust the `--font-size` if you need to.

> If the font is not working correctly, then double-check
> the font name that you have provided in Step 8.
> Please make sure that the font name is the same as shown by Google Font
> during Step 5 and 6 (the font name that was shown to you when you followed Steps 5 and 6).
> 
{style="warning"}

And now the new font(s) should be applied.
