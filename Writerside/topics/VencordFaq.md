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

#### Alternatively, if you want to use a downloaded font:

* Host the font somewhere. [GitHub](https://www.github.com) is a good place.

* For GitHub, all you have to do is create a new repo and upload the font there.

* After clicking on the font file and get the **RAW** link of that.

* Now just like in the previous Step 7, we import the font, but this time
  use the **RAW** GitHub link instead of the Google font approach.

```css
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');
```

instead, it will be

```css
    @font-face {
    font-family: "Font Name"; /* Replace with the name of the font here */
    src: url("RAW GitHub Link"); /* Replace with the hosted github raw link*/
}
```

### 3. How to change the font size?

* Go to `Settings` > `Themes` > `Edit Quick CSS`.

* Find the css variable `--font-size` and change it to your needs.

That's it.

### 4. How to change the accent color (*The Below **RED** thing/part* see attached screenshot)?

<img src="mention_stuff.png" alt="wq is loading" border-effect="rounded"/>

* Go to `Settings` > `Themes` > `Edit Quick CSS`.

* Find the css variables `--accentcolor`, `--accentcolor2` and change them to your needs.

* You may want to play around with them to find the right balance.

> Must-need to change both for it to take full effect.
>
> **Note**: `--accentcolor` is for [rgb](https://rgbcolorpicker.com/) and `--accentcolor2` is
> for [hex](https://colors-picker.com/hex-color-picker/).

{style="warning"}

### 5. How to change the theme welcome username?

* Go to `Settings` > `Themes` > `Edit Quick CSS`.

* Find the css variables `--user-name` and change it.

### 6. How to make it so that desktop `wallpaper/wallpaper engine's` wallpaper is visible through?

> **We recommend you to not go for that**

{style="warning"}

However, if you have decided to make up your mind, then

* Go to `Settings` > `Vencord` > `Enable Window Transparency` and turn it on.

* Now `Settings` > `Themes` > `Edit Quick CSS` and remove `--wallpaper` css variable
  mentioned in [here](#1-how-to-change-the-background-background-image-of-chillax).

* Your window should now be `transparent` or `see through` etc.

* Now you may want to add a bit of blur to make things readable in the `container__037ed`.
  However, discord uses electron, and we have found it to work differently on different
  OS, and the window manager of your OS also plays a vital role here.
  So, the below css snippet may or may not work properly (Translucence is enabled in
  window manager level).
  In case it does not work, it will at least make the `container__037ed`
  basically that region a bit darker.
  ```css
    .container__037ed {
          background-color: rgba(255, 255, 255, 0) !important; /* Semi-transparent white for light theme */
          /* Or use this for dark theme: background-color: rgba(0, 0, 0, 0.1); */
          backdrop-filter: blur(1px) !important; /*Blur the background*/
          border-radius: 10px; /* Rounded corners */
          /* Or use this for dark theme: border: 1px solid rgba(0, 0, 0, 0.2); */
          box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37) !important; /* Optional: Add a box shadow for depth */
    }
  ```

> **Note**: *Linux users this may be a hit or miss due to infinite number of factors
> (Too many DEs, WMs & Display Protocols).*
> But using WM you can **natively add/force** translucence
> at window level
> (i.e. [hyprland](https://hyprland.org/),
> [qtile](https://qtile.org/), [KWin](https://userbase.kde.org/KWin) etc.),
> and you won't have to do any of the above-mentioned things.
>
{style="note"}

### 7. How to change the font of the group chat?

* We have already mentioned how you can import a custom font and
  use it [here](#2-how-to-change-use-another-font-s).

* Now use the below css snippet (*pate it at the **very bottom***):

> If the below css does not work,
> then please create an [Issue](https://github.com/warrayquipsome/Chillax/issues) or report in
> the [Support Discord Server](https://discord.gg/DrfX6286kF).

{style="note"}

  ```css
    /* Reset groupchat name font */
.input_f8b740 {
    font-family: var(--font-name) !important; /* Write the font name here */
    font-weight: inherit !important; /* Self explanatory */
}
  ```

* If you want, you can replace `var(--font-name)` with your custom font name
  if you are planning on using multiple fonts at once.

### 8. CHILLAX is laggy or slow, very slow, any fix?

* Make sure that **Hardware Acceleration** is on.
  If not, then turn it on.

* The steps are first `settings`, then `Advance` and then turn on `Hardware Acceleration`.

*Almost 99% of the time this is the reason behind lag.*

If you are on a system that is not older than six or seven years,
the theme should work fine without any lag.

However, as a last resort you can

* The steps are first `Settings`, then go to the `Themes` Section and then `Edit Quick CSS`.

* [Uncomment](https://developer.mozilla.org/en-US/docs/Web/CSS/Comments) line `37` different/or which
  says `/*@import url("https://warrayquipsome.github.io/Chillax/Addons/SimpleLessLag.css");*/`
  See the below screenshots:

1.  <img src="lag_stuff_1.png" alt="whatever" border-effect="rounded"/>

    * Uncomment this line, and it should look something like the below
      screenshot:

2.  <img src="lag_stuff_2.png" alt="whatever" border-effect="rounded"/>

* This should make it a little less laggy.

Consequently, you can try out [OpenAsar](https://openasar.dev/) which is part
of the [Vencord installer](https://github.com/Vencord/Installer/issues/11).
This should give a bit more performance boost.

### 9. How to make the member list always stay visible instead of on hover?

This is basically an addon; to remove it:

* The steps are first `Settings`, then go to the `Themes` Section and then `Edit Quick CSS`.

* **Remove** or **comment out** the line (*currently line number `33` and maybe different in your case*) containing
  `@import url("https://warrayquipsome.github.io/Chillax/Addons/AvatarOnlyMemberList.css");`.
  Now the member list will always be visible instead of on hover.
  See the below screenshots:

1.  <img src="always_visible_member_list.png" alt="wq is loading" border-effect="rounded"/>

    * Now remove/comment out this line.

2.  <img src="commented_out.png" alt="wq is loading" border-effect="rounded"/>

    * Finally, you should have something like this:

3.  <img src="results.png" alt="wq is loading" border-effect="rounded"/>

### 10. How to get back the old emojis?

This is also very similar to the previous [FAQ](#8-chillax-is-laggy-or-slow-very-slow-any-fix).
This thing is also an addon.
Remove it to get back default emojis:

* The steps are first `Settings`, then go to the `Themes` Section and then `Edit Quick CSS`.

* **Remove** or **comment out** the line (*currently line number `29` and maybe different in your case*) containing
  `@import url("https://mwittrien.github.io/BetterDiscordAddons/Themes/EmojiReplace/base/Microsoft.css");`.

* Now you should have the old emojis.

### 11. How to get rid of the Folder Icons and Make it like the old discord?

* The steps are first `Settings`, then go to the `Themes` Section and then `Edit Quick CSS`.

* **Remove** or **comment out** the line (*currently line number `34` and maybe different in your case*) containing
  `@import url("https://warrayquipsome.github.io/Chillax/Addons/FolderRedesign.css");`.

* Now it should be normal like the old discord.

### 12. How to get rid of the below-attached ugly thing?

<img src="ugly_writing_white_bg.png" alt="wq is loading" border-effect="rounded"/>

* The steps are first `Settings`, then go to the `Themes` Section and then `Edit Quick CSS`.

* Now the use/paste below css snippet at the very end:

> If the below css does not work,
> then please create an [Issue](https://github.com/warrayquipsome/Chillax/issues) or report in
> the [Support Discord Server](https://discord.gg/DrfX6286kF).

{style="tip"}

If you are using dark mode, then the below css snippet

```css
    /* hide message in the sidebar when using dark mode */
.theme-dark .sidebar_a4d4d9 .content_eed6a8:after {
    color: rgba(255, 255, 255, 0) !important;
    text-shadow: none !important;
}
```

Or, if you are using light mode, then the below css snippet

```css
    /* hide message in the sidebar when using light mode */
.theme-light .sidebar_a4d4d9 .content_eed6a8:after {
    color: rgba(255, 255, 255, 0) !important;
    text-shadow: none !important;
}
```

* Now it should be a bit better.

### 13. How to use dark/light mode in Chillax Theme?

You can enable `dark` or `light` mode from the Discord Settings.
Steps are:

* Now go to `Settings` > `Appearance`.

* Finally, choose either light mode or dark mode based on your preference,
  and Chillax will reflect that.

### 14. After applying Chillax theme it looks funny and/or transparent/see through background is missing, what to do?

Before applying the theme:

* Firstly, make sure that there is **no custom** css or css snippet(s) is/are running.

* Secondly, make sure that no party plugin related to theming
  is running (*if debugging, disable all plugins for quicker conclusion*).

* Thirdly, `Settings` > `Appearance` is set to either Dark or light mode.

* Now apply the Latest version
  of [Chillax](https://raw.githubusercontent.com/warrayquipsome/Chillax/main/chillax.theme.css).

* Now you should have Chillax with the default look and feel.

### 15. How to get rid of the mobile icon besides the avatar?

* The steps are first `Settings`, then go to the `Themes` Section and then `Edit Quick CSS`.

* Now to the line `92` or find the line that says `--rs-phone-visible: block;` and
  change this line to the below line:

    ```css
        --rs-phone-visible: none;
    ```

* Now mobile icon or phone icon should be gone.

### 16. How to change the color of urls/links?

* The steps are first `Settings`, then go to the `Themes` Section and then `Edit Quick CSS`.

* Now apply the below css snippet, which will change the color of every
  url to the color of your choice.

```css
    [href^="http://"], [href^="https://"], [href^="www."] {
        color: #30d944 !important; /* change it to whatever you like */
    }
```

## Still Have Question(s)?

Join our support
<format color="#ffA36b">
        [Discord Server](https://discord.com/invite/DrfX6286kF)
</format>
and ask for help and do not be <control>shy.</control>