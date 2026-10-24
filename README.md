# Little Coders

Make games, earn coins, play games. A coding playground for kids that goes from blocks to real code.

Kids build a game by snapping blocks together, peek at the JavaScript the blocks make, and switch to typing that code themselves when they are ready. Finishing a game earns coins. Coins buy other coders' games from the Game Shop, and a finished game can be published there at a price the maker sets.

**Try it:** https://dfings.github.io/little-coders/

## This is a mock-up

Nothing here is backed by a server. The coins, the shop and the other coders are all pretend:

- Everything is saved in the browser's local storage, so it stays on one browser on one computer.
- The six games in the shop are built into the page.
- Published games get "bought" by simulated coders while the page is open.

## Running it

Open `index.html` in a browser. There is nothing to install or build, and no server.

## How it works

- **Make.** A new game starts with a cat you can move with the arrow keys. Add blocks from the palette, press **Play** to try it, and use **Undo** and **Redo** freely.
- **Blocks to real code.** **Peek at the real code** shows the JavaScript behind the blocks. **Real code** turns the blocks into code you can edit. Going back to blocks does not convert typed code; the blocks stay as they were.
- **Finish.** Win your own game once, then press **Finish game** to earn 25 coins (10 for a remix). You can keep editing afterwards.
- **Publish.** Put a finished game in the Game Shop for free or for up to 30 coins. Untick **Let other coders look inside and remix it** to keep buyers from opening a copy. Edits to a published game go live straight away.
- **Game Shop.** Buy games with coins. You start with 10.
- **My Games.** Every game you made or bought. **Look inside** opens a copy of a bought game in the editor to remix, unless its maker turned that off.

## The stage

The stage is 480 wide and 360 tall. `x` goes from 0 on the left to 480 on the right, and `y` goes from 0 at the top to 360 at the bottom. In real code those edges are `X_MAX` and `Y_MAX`.

A small game in real code:

```js
background('skyblue');
make('🐱', 'cat', 240, 280);
makeMany(4, '⭐', 'star');

whenKey('left',  () => { move('cat', 'left', 5); });
whenKey('right', () => { move('cat', 'right', 5); });
whenKey('up',    () => { move('cat', 'up', 5); });
whenKey('down',  () => { move('cat', 'down', 5); });

whenTouch('cat', 'star', () => {
  goRandom('star');
  changeScore(1);
  sound('coin');
});

whenScore(10, () => {
  win();
});
```

The palette on the left of the code editor lists every function you can use.

## Health, hunger and hiding

- **Health and hunger** are two separate meters on every character. Both start at 10 and appear above the character, as ❤️ and 🍗, once a block changes them. The blocks can take away, add, or set a number. **When health of … reaches** and **when hunger of … reaches** run when a meter lands on or passes that number, going up or down. In real code: `setHealth`, `changeHealth`, `health`, `whenHealth`, and the same for hunger.
- **Invisible** characters are not drawn and cannot touch anything or be tapped, but they still move and count. In real code: `hide('cat')` and `show('cat')`.
- **If … is N spaces or closer to …** runs the blocks under it in the stack only when the two are that close. Spaces are measured edge to edge, so 0 means touching. Blocks under an **if** are indented. In real code: `if (distance('cat', 'ghost') <= 50) { … }`.

## Saving and loading

Because saved data lives in one browser, files are the way to back up work or move it to another computer.

- **One game.** **Save to file** in the editor, or the 💾 button in the workshop. Load it with **Load a game from a file** in the workshop.
- **Everything.** **Save everything to a file** and **Load everything from a file** in the footer cover all games, coins and the profile.
- **Codes.** **Get a code** turns everything into a block of letters you can copy and paste, for example into a message to yourself. **Use a code** loads it on another device. A code is the save file, compressed and base64-encoded, so a file that contains a code loads too.

The welcome pop-up can also start from a saved file or a code.

A real-code game loaded from a file runs whatever JavaScript is in it, so only load files you trust.

## License

MIT. See [LICENSE](LICENSE).
