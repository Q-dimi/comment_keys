# comment-key

Comment-key will search through all your directories and files looking for comments with a specific syntax. Specifiy one directory and all inner directories and files will be checked.

```sh
npm install comment-key
```

# Syntax

```js
//^*^(your comment here)
```

# Examples

```js
//^*^(add a button here)

/*
  please make sure to add a button that updates the shopping cart
*/

//^*^(update this regular expression)

/*
  update the regular expression to accept numbers 1-9
*/

//^*^(Im not sure what this is? can someone please explain in this key)

/*
  im not sure what this function does...
*/

//^*^(I do not understand. someone send an email to jdoe@mail.com)

/*
  I dont know how this works. Can someone send me an email.
*/
```

# Getting Started

```js
const comment_keys = require("comment-key");

/*
   { folder: './my_folder', files: ([]), ('all'), (['a.js', 'b.js']) }
   'all' searches through all directories and files
*/

const folders = [
  { folder: "./cron", files: "all" },
  { folder: "./db", files: "all" },
  { folder: "./routes", files: "all" },
  { folder: "./public", files: "all" },
  { folder: "./views", files: "all" },
  { folder: "./", files: ["app.js"] },
];

var comments = [];

try {
  comments = comment_keys(folders);
} catch (err) {
  console.log(err.message);
}

for (let i = 0; i < comments.length; i++) {
  console.log(comments[i]);
  //filepath
  //linenumber
  //comment
}
```

# Use case

- You are a manager going through all of your files and making updates. You write comments everywhere with the syntax (above) so that your devs can see the list of comments, know where to go and what they need to do. After your devs work on their keys, you as a manager host a zoom call the next day and ask everyone how their comment keys went. _ You are a junior who is stuck on a problem so you leave a comment key with your email and the question you have. _ You are clicking around in your application and find a few bugs so you write some comment keys to handle them later.
  Below each comment you should have a larger comment without the syntax that describes what the problem is in detail.

# How it works

Uses the file system module to traverse a set of directories looking for '//^\*^('. Once '//^\*^(' is found, the comment gets built up and is pushed to the comment set.
