### Define a Constructor and Initialize Properties

* let epicFailVideo = function(epicRating, hasAnimals) {
    this.epicRating = epicRating;
    this.hasAnimals = hasAnimals;
}

let parkourFail = new epicFailVideo(7, false;
let corgiFail = new epicFailVideo(4, true);

console.log(parkourFail);
console.log(corgifail);

* let epicFailVideo = function(epicRating, hasAnimals) {
  this.epicRating = epicRating;
  this.hasAnimals = hasAnimals;
}

epicFailVideo.prototype.generateRandom = function(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

let parkourFail = new epicFailVideo(7, false);
let corgiFail = new epicFailVideo(4, true);

console.log(parkourFail.generateRandom(1, 5));
console.log(corgiFail.generateRandom(1, 5));

* let epicFailVideo = function(epicRating, hasAnimals) {
  this.epicRating = epicRating;
  this.hasAnimals = hasAnimals;
}

epicFailVideo.prototype.generateRandom = function(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

epicFailVideo.prototype.dailyLikes = function() {
  let viewers, percentage;

  viewers = this.generateRandom(10, 30) * this.epicRating;

  if (this.hasAnimals) {
    percentage = 0.75;
  } else {
    percentage = 0.40;
  }

  return Math.round(viewers * percentage);
}

let parkourFail = new epicFailVideo(7, false);
let corgiFail = new epicFailVideo(4, true);

console.log(parkourFail.dailyLikes());
console.log(corgiFail.dailyLikes());

* let epicFailVideo = function(epicRating, hasAnimals) {
  this.epicRating = epicRating;
  this.hasAnimals = hasAnimals;
}

epicFailVideo.prototype.generateRandom = function(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}

epicFailVideo.prototype.dailyLikes = function() {
  let viewers, percentage;

  viewers = this.generateRandom(10, 30) * this.epicRating;

  if (this.hasAnimals) {
    percentage = 0.75;
  } else {
    percentage = 0.40;
  }

  return Math.round(viewers * percentage);
}

epicFailVideo.prototype.weeklyLikes = function() {
  let total = 0;

  for (let i = 0; i < 7; i++) {
    total += this.dailyLikes();
  }

  return total;
}

let parkourFail = new epicFailVideo(7, false);
let corgiFail = new epicFailVideo(4, true);

console.log(parkourFail.weeklyLikes());
console.log(corgiFail.weeklyLikes());

## Basic table Structure 

* table
* tr
* td

##Table Headings

* th

## Long Tables

* thread
* tbody
* tfoot

## 