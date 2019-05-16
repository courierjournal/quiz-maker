# quiz-maker

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```


### Quiz templates
Assigned by setting `quiz.template` in the data.json file.

* `boolean` - Simple true/false based quiz. By default the choices are displayed as "True" and "False". But these can be overridden with custom text.
* `multiple-choice` - Multiple answers to choose from, only one answer is correct.
* `multiple-choice-show-answer` - Same as multiple choice, but highlights the correct answer and shows optional chatter. Requires the user to manually click to get to next answer.
* `multiple-choice-weighted` - Same as multiple choice but answers are usually opinion based and therefore no single one is correct. The result is weighted in favor of the index of the chosen answers and the result is a category. If the even there is a tie because the user picked an even number of answers, a random result is chosen.
* `decision-tree` - A node based tree where questions are deterministic based on prior answers. A question can have any number of answers. In a decision tree, all answer forks are unique and cannot reference another branch.
* `graph` - Similar to a decision-tree but answers are able to reference questions in a different or prior branch.
* `name-generator` - Given 2 different inputs, generate a first and last name.


### Results templates
* `percent-banner` - Display the percent in big bold words up top
* `custom` - Passes custom HTML into the results container

### Options
* `confettiMode` - splash confetti on the results screen. Triggers where user got >=70% of the questions correct OR triggers all the time on templates that have no correct answers.
* `familyFeudMode` - It's time... to play... THE FEUD! Make sure your speakers are on.
