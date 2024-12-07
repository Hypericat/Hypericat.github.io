---
layout: default
---
# Wordle Solver

## Development
This project was very much a quick and dirty solver because I suck a Wordle. The bulk of this was written within one night, while I had nothing better to do. The solver takes in a file with all the 5 letter words within the english alphabet. It reads them all in and ranks each letter with a score base on how frequent it was seen. The program keep tracks of letters that musn't appear within the word and removes all words containing them. It suggests the best word by finding the word who's characters have the highest score. Corrrect letters are represented with captitals, letters that the word contains but not in that exact position are lower case and incorrect letters are prefixed with a hyphen.

## Additional Features

The previous version worked, but it was slow and inefficient. The code was modified to have two modes. The first would attempt to narrow down the word list as much as possible, using the most letters who's state we do not know (We don't know whether they are used or not) until the list of possible words is below a small threshold. At this point we switch back to the orignal method and return the most likely result.

<style>
.button {
  border: none;
  color: white;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

.repo {
 padding: 8px 25px;
 background-color: #008CBA;
} /* Blue */


.repo {
  background-color: white;
  color: black;
  border: 2px solid #008CBA;
}

.repo:hover {
  background-color: #008CBA;
  color: white;
}

.back {
  padding: 12px 100px;
  background-color: #aa0405;
} /* Red */

.back {
  background-color: white;
  color: black;
  border: 2px solid #aa0405;
}

.back:hover {
  background-color: #aa0405;
  color: white;
}
</style>

<a href="https://github.com/Hypericat/Wordle-Solver"> <button class="button repo">Visit Repository</button></a>

<a href="./"> <button class="button back">Back</button></a>