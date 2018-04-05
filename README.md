# TextBar Scripts

This is my personal collection of scripts for use with [TextBar](http://richsomerfield.com/apps/textbar/). **TextBar** is a great application for putting small scripts with useful information at your finger tips in the menu bar. Some of these are scripts that I first made for [BitBar](https://getbitbar.com/). Others use the unique features of **TextBar**. Have fun!

## TodoNotePlan

This is a port of my [BitBar](https://getbitbar.com/) script by the same name. It will display the current days todo items from [NotePlan](https://noteplan.co/). It works with my [Alfred NotePlan Workflow](https://github.com/raguay/MyAlfred/blob/master/Alfred%203/NotePlanWorkflow.alfredworkflow).

## TaskPaperTodo

This script displays the current days todo item in the [TaskPaper](https://www.taskpaper.com/) program for the macOS. The items are color coded based on the tags for the todos. You can edit the colors by editing the script. You have to set the file location of the **TaskPaper** file you want to use.

This script complements the [Alfred ToDo Workflow](https://github.com/raguay/MyAlfred/blob/master/Alfred%203/TodoWorkflow.alfredworkflow) in my [GitHub Alfred repository](https://github.com/raguay/MyAlfred)

This is a port of the same script for [BitBar](https://getbitbar.com/).

## Current Files and Editor

This script displays a list of often edited files and editors that you use. These are in the files: ~/.myCurrentFiles (one file per line of files you want to appear in the list), ~/.myeditorchoice (The current editor you have selected to use), and ~/.myeditors (List of editors you use. Text name with a pipe symbal and then the path to the editor).

I use the Alfred Workflow [My Editor Workflow](https://github.com/raguay/MyAlfred/blob/master/Alfred%203/My%20Editor%20Workflow.alfredworkflow) to edit and add things to these files.

## Dir Listing

This is an example of using a simple node based web server to give information to the webview in TextBar. You can browse your directories and files in the webview. It is actually very handy!

This one requires you have have node.js installed on your system. The easiest way for that is by installing it with [Homebrew](http://brew.sh).

## NotePad

This is another example of using a node based web server to give information to the url view in TextBar. This is a 5 pages of notepad to switch back and forth. It currently doesn't have a history or undo feature. It will save the notes to a file in your home directory called `~/.notesjson`. 

It has scripts that it keeps in the file `~/.scriptsjson`. You can select some text, press `<ctrl>-m`, select the script from the menu that pops up (the menu is scrollable to see all the scripts. It also has a search box to narrow down the selections. You can then use up and down arrows to select one.), and that script will be executed. If you don't select some text first, the script is applied to all the text in the current note. It currently has 27 scripts. Let me know if there is a script you really need!

If you update the version of this script, you will have to remove the `~/.scriptsjson` to see the newly added scripts. I'm working on a way to add them without this step.

There is a red button on the bottom for stopping the server. You can then restart the server by reloading the script. I use this all the time in the testing of new features.

You have to have node.js installed on your system to run this script. The easiest way for that is by installing it with [Homebrew](http://brew.sh).

More features to come. Stay tuned!

### Math Features

The notepads now have scripts for processing math: the 'Basic Math' and 'Evaluate Page for Math' scripts. The 'Basic Math' script is for processing arbitrary pieces of math in a selection. The 'Evaluate Page for Math' script is for processing the entire note with a nice running result along the right. The 'Basic Math' script doesn't reset the state of the math library (ie: variable definitions and functions), but the 'Evaluate Page for Math' does each time invoked so as to not create multiple copies of function and variables.

Copy the following note to a notepad:

```markdown
# Using the ‘Evaluate Page for Math’ script

Your notes can have any text you need. But when a line starts with a ‘>’, that whole line is processed for math. The line is processed and the answer pushed to the right with a ‘|’ symbol.

> 6 * 95
> x=6*8-10
> x

Text in the middle doesn’t clear out the variable or function assignments before it.

> f(x)=x^2-5*x+12
> f(60)
> f(x)

The length of the note isn’t a concern either.

> f(100)

> bank=34675
> check=5067
> balance = bank - check

> sin(45)

The math package used doesn’t do conversions or symbols inside of the math expressions. The math library used is [mathjs 4.0](http://mathjs.org/).
```

Then press `<ctrl>-m` and select the 'Evaluate Page for Math' script. Each line with the '>' as the front character now has the results to the right. When you change the text lines and re-run the script, the math lines are all updated. All other lines are not effected by the script. You can change any equation or variable and it's effects will trickle down the page.

### Making Scripts

All scripts have to get the text to process from `global.NP.text` and place the new text back into the `global.NP.text` variable. For example, in a note, place the following code:

```javascript
try {
   var lines = global.NP.text.split('\n');
  global.NP.text = '';
  for(var i = 0; i < lines.length ; i++) {
      var match = lines[i].trim().match(/^\d+\. (.*)$/);
    if (match != null)
        global.NP.text += match[1] + '\n';
  }
} catch (e) {
   global.NP.text += "\n\n" + e.toString()
}
```

Then go to a different note and place several lines of text. Run the script `Bullet lines with Numbers`. Every line will have the proper number at the front of it. Now, run the script `Evaluate Note # as Script` with `#` the number of the note you put the script. The numbers at the beginning will now be removed!

You can access the following libraries also: `global.NP.moment` for [moment.js library](https://momentjs.com/), `global.NP.mathjs` for the [math.js library](http://mathjs.org/), and `global.NP.jQuery` for the [jQuery.js library](https://jquery.com/).

### Known Issues

If you change notes and press undo, `<cmd>-z`, you will get the last notes in the current notes.

When first installing the script, the server will not be able to register the port (a weird edge case with the first use of the script). If you see a white screen with a server error message, press the red button twice (first time is to select the window. Even though you have focus for typing, you don't have focus for clicking.) and then reload. You should be requested to let the server open the port or not. You only get this the first time the server launches.

### Coming Features (Not in any particular order):

- Editing and adding new scripts.
- Better colors and theming (partially done).
- Regular expressions selecting and editing of notes.
- Storing regular expressions for future use.
- Add new scripts without having to remove the script store.
- Make a PopClip, Alfred, LaunchBar, and Dropzone 3 scripts for adding to the notes.
- Fix the XML errors when saving notes to the server.
- Undoing after changing notes puts all the notes from the last note into the current note. Need to clear out the undo buffer when changing notes.

If you have something you would like to see, just make an issue with the tag `[Features][NotePad]` in the subject and I'll see what I can do.

### Features that have been added or fixed

- It will now come up showing the first note without having to press the bottom button.
- When you change notes, the text area will get input focus right away without having to click on it.
- Cursor now is set to the end of the area changed by a script.
- Math features have been added using the math.js library.
- Added many time and date based scripts using moment.js library.
- Scripts that work on the whole note or just the selection.
- Pop-up menu of available scripts with an input for condensing the number of items by only showing script names with the letters typed in it. Then you use the up/down arrows to select one and `enter` to run the script. Or, you can scroll and click the desired one.
- A button (red) to stop the node.js server.
- Full text editor support with color highlighting (markdown) and my own theme.
- Re-factored to use the [CodeMirror](https://codemirror.net) editor instead of a plain textarea.
- The script menu now has a focused input to narrow down the list with text given. Then you can use the up and down arrow keys to select the script you want to use.
- You can now write a script in a note, switch to another not and select some text, and run the 'Evaluate Note # as a Script' where # is 1-5. The selected text is in `global.NP.text`. You can access the following libraries also: `global.NP.moment` for moment.js library, `global.NP.mathjs` for the math.js library, and `global.NP.jQuery` for the jQuery.js library. These things can change as I work to make this a better program.
