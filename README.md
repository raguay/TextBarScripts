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

This is another example of using a simple node based web server to give information to the url view in TextBar. It gives you a 5 pages of notes to switch back and forth. It will save the notes to a file in your home directory called `~/.notesjson`.

More features to come. Stay tuned!

### Known Issues

Currently, first time to run, you will have to select a note by one of the colored dots at the bottom. The first note isn't selected properly with TextBar, but works fine in a full browser.

### Coming Features:

- Running scripts on full notes or just the selection.

If you have something you would like to see, just make an issue with the tag [Features] and I'll see what I can do.

