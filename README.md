Colejak 
=======

The programmer's layout.

- Colemak-DH foundation
- Improved for thumb typing
- Evens out left/right usage imbalance
- Homerow symbols through dead keys
- Number Layer
- Navigation row enabling app-agnostic and layout-agnostic Vim motions
- Created for run-of-the-mill staggered keyboards first
- Optimized keyboard shortcut ergonomics

![Layout preview](
https://github.com/jnz1g/colejak/blob/main/assets/colejak.png)

![Layout finger placements](
https://github.com/jnz1g/colejak/blob/main/assets/colejak-finger-placement.png)


Quickstart
----------

### Installation

> [!NOTE]
> These will overwrite existing destination files. Your original files such as *evdev.xml*
will be saved as *evdev.xml.bak*

#### Copy

```
git clone https://github.com/jnz1g/colejak
cd colejak
mkdir --parents $HOME/.config/xkb/rules
mkdir $HOME/.config/xkb/symbols
cp --suffix=.bak rules/* $HOME/.config/xkb/rules/
cp --suffix=.bak symbols/* $HOME/.config/xkb/symbols/
cp --suffix=.bak .XCompose ~/.XCompose
```

#### Symbolic Link

```
git clone https://github.com/jnz1g/colejak
cd colejak
mkdir --parents $HOME/.config/xkb/rules
mkdir $HOME/.config/xkb/symbols
ln --symbolic --suffix=.bak $(realpath rules) ~/.config/xkb/rules
ln --symbolic --suffix=.bak $(realpath symbols) ~/.config/xkb/symbols
ln --symbolic $(realpath .XCompose) ~/.XCompose
```

### Sway

```
set $kb "1:1:AT_Translated_Set_2_keyboard"
input $kb {
    colejak(default)
}
```

### GNOME

Search for *Colejak* in `gnome-control-center > Keyboard > Input Sources`

### Target Users

This layout is made for programmers. As such, it features the following
caveats:

- Optimized for English.
- Uses custom dead key mappings for all symbols.
- Setting up would be easiest on linux or a highly customizable keyboard
firmware like QMK.
- Unofficially supported everywhere.
- High initial learning curve (100 hours minimum).

Recognize if such hyper-optimization is crucial to your workflow. Otherwise,
Dvorak, Colemak, Colemak-DH is highly recommended.

Design Decisions
----------------

- When referring to the layout's statistical performance, it is measured using 
Keyboard Layout Analyzer - SteveP's fork. This means that we have yet to take
into account the usage of modifier, special, arrow, compose, and dead keys.

- The term fingers mean the thumbs are excluded. All 5 fingers on one hand are
referred to as hand. 

### Colemak-DH Foundation

Before choosing a layout, I tried creating one from scratch. I ended up with
something similar to Colemak. I decided to go with Colemak-DH for 2 reasons:

- The middle two keys are somewhat exhaustive to reach for and is especially uncomfortable
with certain same-hand homerow bigrams.
- The new placements of DH take better advantage of thumb typing.

### H/K Swap

KH is only a problem with thumb typing as it places the uncommon K directly
under the thumb and vice versa.

### DFG Rearrangement

The left hand of Colemak-DH feels noticeably more awkward compared to the right
side due to:

- Imbalanced left/right finger usage (thumb excluded)
- Overloaded left thumb
- Underutilized left middle finger especially when compared to its right side
counterpart
- Newfound growing pains with G previously non-existent in qwerty.

#### The F key

The biggest culprit for the finger imbalance, especially in the middle finger pair,
is the overzealous placement of `F`. Based on various sources, it's not in the top 10
most used letters. Compare this to its right sibling which has E, the most
common letter by a landslide, and U, the least common vowel. 

The left middle key a.k.a G was the #1 candidate. I didn't like G's current
placement and I've tried G where F was when I was designing a layout from
scratch. After 24 hours of typing tests, I've not found any awkward bigrams or
word sequences, thus F found its new home. A secondary benefit is that we've lowered the usage of the
borderline overloaded left pointer finger.

We've improved the left middle finger usage but the total left/right finger 
usage imbalance remains as we only swapped existing keys around. We need to take
a key from the thumbs or right side to see concrete differences.

#### The G and D keys

Finding candidates to swap with G, we take a look first at D.

D is the reason why the left thumb is overloaded. Beyond just the percentage
utilization of the left thumb, we also take into account its finger travel. Since
its keys are spread horizontally, any increases in usage is dramatically felt.
In other words, my left thumb was constantly jumping around. Another benefit for
D is that SD is one of the few uncommon bigrams for S.

Perfect. Let's kill two birds with one stone. By swapping G and D, we lower left
thumb usage but kept it high enough to make gains over thumb typing in qwerty
and we balance out total left/right finger usage. (that's a lie, right side
still does 5% more work but this IMO is acceptable and there's more ways
to balance it out further)

### Using Dead Keys for All Symbols

Cons:

- Each period, comma, and whatever else common symbol that you use will all 
take two keystrokes.
- Any behavior involving modifier key + symbol will not work through the dead 
key. 
- This is hard/impossible to setup on Windows and MacOS.
- If you need dead keys for international symbols, you'd be using the worse Compose key which
takes three keystrokes total. Although we do have three dead key types (grave,
tilde, acute) so hopefully you don't run out lol.
- High learning curve
- Some browsers don't respect .XCompose (Firefox LTS on Debian). It does work
in Brave though.

This is a tradeoff that I'm willing to take for:

- Significant increase in accuracy
- Fingers stay at/near homerow

Things to take note of:

- Vim keybinds and any application keybinds with symbols still work as long
as it's the symbol alone. This means typing ":" in vim through dead keys
still bring up the command line. In some websites however, this is finicky. 
(Discussed later)
- A lot of symbol keys near the right pinky and some keys on the number row
are left unchanged. Take advantage of these to suit your needs.

Found inside `.XCompose`

### Number Layer

Cons:

- `Modifer key + number` such as `Ctrl + 1` won't work with this layer. A workaround
would be to have a Colejak variant. A.k.a you switch layouts everytime you want to
use numbers and switch back. (barf) 
> [!NOTE]
> On Sway, you can add `Mod5` to your config. `Mod4 + 1` -> `Mod4 + Mod5 + 1`

- There's not any good places left on the keyboard to activate the number layer.
I myself don't like its placement either but I'm hoping an ergonomic keyboard
can remedy this.

Found inside `symbols/colejak`

### Navigation Row

We've now essentially brought the number row to the home row. This unlocks
a whole row for remapping. What better keys to map than to place navigation-related
keys here. Pros:

- Layout agnostic hjkl movemet + Home/End (no more getting confused with gg and G!).
- Arrow keys enable vim motions in **ALL** applications and textboxes.
- Vim motions in insert mode(??? for the lazy a.k.a me)

Especially within textboxes, here are available motions beyond hjkl:

- Word skipping - `Control+arrow`
- Start/End of a line - `Home` / `End`
- Start/End of textbox - `Control+Home` / `Control+End`
- Visual mode  - Hold shift while doing all the goodies above.

Honestly, this is my favorite feature of the layout. If I somehow go back to qwerty,
I'd still implement this.

### Slash, Multi_key

- A quirk to know about symbols is that the layer they are in for qwerty matters
alot in the consistency of their keybind behavior across various applications. I tried
placing Escape on the shift layer. Sometimes, apps see this as `Shift+Escape`
and noop it which forces you to reach for the original Escape anyway. Since slash
is on `Shift+dead_grave`, I gave it another key where its on the base layer. Although
I've never had behavior consistency troubles with slash on the shift layer.

- There's no Multi_key in the .XCompose file but I put it here since I have nothing
else to place here. If you need it, here you go.

> [!NOTE]
> You can find more quirks and how they affect implementation and design decisions
in the source files' comments.

### Control, 2 Shifts, Enter, Backspace, Del, Escape

These are the modifier and special keys that I consider essential. There's
no philosophy behind the placements beyond finding the least inconvenient one.
Here's what I kept in mind while juggling these.

Control - Colemak places backspace here. I think that's too good of a
placement for backspace. I value ergnomics of keyboard shortcuts much more.

Backspace - Keep it on the opposite side of Control for `Control+Backspace`
and don't make the poor pinkies be responsible for mashing this key.

Right Shift - I previously only used left shift but on this Colejak journey,
I've come to realize how much more ergonomic having right shift is. Also,
keep it near the arrows for `Control+Shift+Arrows`

Escape - Keep it near the arrows because when I only have one-hand on the 
keyboard, I often find my cursor still focused in some ui element.

Delete - Keep it somewhat out of way so that if im in my file
manager, I don't just accidentally nuke a folder/file.

Right Control - It was either this or Right Shift. I felt that Right Shift had
much more ergonomics than what Right Control had to offer. Most keyboard shortcuts
from qwerty have left control in mind anyway.

Enter - Just trust me on this one. It's actually decent lol. There's nowhere else
to place it!! Also, I originally had it where `Right Shift` is since my Qwerty
days but here in Colejak, I find myself mixing up `O` and `Enter` alot which is
notably annoying in vim's netrw.


FAQ
---

### What are dead keys and Compose keys?

Think of these as combo keys. Dead keys are two-combo keys while the Compose
key is three-combo key. Dead keys are usually used for international symbols.
There's three types of combo keys (grave, tilde, acute) - not to be confused
with the normal grave and tilde keys. For example, pressing `dead_tilde+n`
outputs ñ.

### How do I take full advantage of this layout?

- Use vim motions in your editor
- Install vimium in your browser
- Use a tiling window manager
- Install warpd

You'd reach for the mouse maybe 1-20 times a week. And if you're on a
laptop, the trackpad is literally within thumb's reach. Guaranteed productivity
gains.

### How would I go about practicing this layout?

- I did it in 3 weeks with my brain turned off. Literally just typed my brains out.
I average 100wpm after 50 hours of typing tests. Add about 10 hours more to get 
used to keyboard shortcuts. Here's how I did it.

    - Monkeytype English until 50 wpm average.
    - Keybr. Apply these settings (a) 60 wpm target speed. (b) Unlock next key only 
    when the previous keys are also above the target speed. Beat all letters.
    - Monkeytype English 5k until 80 wpm average.
    - PR 132 wpm on Monkeytype English.
    - Monkeytype code rust for numbers and symbols
    - Monkeytype quotes
    - Monkeytype code javascript for common programming words

### Does this apply to TTY as well?

No. And I don't recommend doing anything this complicated to your TTY
settings... ***here be dragons***

TODO
----

> [!WARNING]
>  Subject to Change (Modifier keys, Special Keys, XCompose, Num Layer)

- Add statistics from keyboard layout analyzer.
- Indicate sources of character/bigram frequencies. (English + Programming)
- Add comments in xkb files (experimental features, implementation details)
- Indicate Num Layer in keyboard previews once its finalized
- Contribute layout to monkeytype

Contribution
------------

- Optimize the .XCompose mappings.
- A better num layer?
- Issues about the documentation are encouraged. (Something is confusing or
calls for a more in-depth explanation)

Resources
---------

[XKB Configuration Files Documentation](https://www.charvolant.org/doug/xkb/html/node5.html#SECTION00054000000000000000)

[Libxkbcommon commit: Allow for custom rulesets through include files](https://github.com/xkbcommon/libxkbcommon/pull/108/commits/bc4a691cb9f45c3309c78c997e00212f0978d082)

[Setting up $HOME/.config/xkb/](https://who-t.blogspot.com/2020/02/user-specific-xkb-configuration-part-1.html)

[Creating evdev.xml](https://who-t.blogspot.com/2020/07/user-specific-xkb-configuration-part-2.html)

[Extending system layouts with custom variants](https://who-t.blogspot.com/2020/08/user-specific-xkb-configuration-part-3.html)

[Youtube video where I discovered the blog posts from](https://www.youtube.com/watch?v=utqpa_8SXkA)

[This only works on Wayland and XWayland](https://who-t.blogspot.com/2020/09/no-user-specific-xkb-configuration-in-x.html)

[Where I discovered about XCompose and Dead Keys (DreymaR's Big Bag)](https://dreymar.colemak.org/)

Acknowledgement
---------------

### Keyboard Layout Pictures
- Created with [keyboard-layout-editor.com][keyboard-layout-editor]. 
- JSON for all layouts are available in [assets][assets].
- Layout typing performance measured with [ Keyboard Layout Analyzer - SteveP's fork ][keyboard-layout-analyzer]

### KCX Qwerty

- [ KCX Qwerty ][kcx-qwerty] is my old layout. Improved with modifier/special keys closer to the homerow.
This instead extends the default `symbols/us(basic)` layout which some may find useful.

[keyboard-layout-editor]: http://www.keyboard-layout-editor.com/
[assets]: https://github.com/jnz1g/dotfiles/tree/master/.config/xkb/assets
[keyboard-layout-analyzer]: https://stevep99.github.io/keyboard-layout-analyzer/#/main
[kcx-qwerty]: https://github.com/jnz1g/kcx-qwerty
