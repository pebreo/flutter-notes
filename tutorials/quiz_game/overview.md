# Writing a Quiz game in Flutter

In this tutorial, we will create a simple quiz game called "The Quizz".
When first learning a framework, it is best to start simple. In this tutorial,
we will start with the basics of Flutter such as : widgets, tk.
If you are coming from Javascript or Python, there are certain things that 
will look familiar to you like: arrow functions, classes, and the `var`
keyword. I will try to explain in as much detail about the Flutter API
so you get some insight.??
This tutorial assumes that you have some a little programming experience
but not necessarily familiar with Dart language or Android development.

## The Quiz - General Algorithm

We start with the general algorithm of the program. Our quiz
program will have 3 pages: the landing page, the quiz page,
and the score page.

Each page will have it's own `.dart` file and inside of each
file we will write classes that define the layout as
well as the logic. In Flutter, the layout and logic are encapsulated
in so-called widgets. 99% of the time you will deal with two widget classes:
`StatelessWidget` and `StatefulWidget`. 

The `StatelessWidget` is tk.

If we want to tk, we will need to use the `StatefulWidget` class. 

The general logic for the entire app will be:

* When the user starts the program, they will be shown a landing page that
says: "The Quiz". The user will then tap the screen where they will be taken to the next page.
The file involved for page are: `/pages/landing_page.dart`.

* And the next page is the Quiz page. Most of our data structure and logic code
will be dedicated to this page. 



If you've ever looked at Android code and felt daunted, you will be relieved that
a basic app in Flutter is easier to grasp, at least from a web developers point of view.
For a high-level project view, here is a list of the files involved. 

The files can be categorized into 3 categories: the data model, the UI, and the logic.
This categorization has a special acronym for it: MVP which stands for Model View Presenter.
The model corresponds to the data model, the UI corresponds to the Presenter, and the
View corresponds to the logic.

The files involved in the data model are:

    utils/question.dart - a Dart class that will contain a String and bool
    utils/quiz.dart - a Dart class that contains a List and number as well as some getters

Notice that we break down our data model into two pieces: a question and a quiz. 
We implement the quiz as a collection of questions. In this tutorial, we will just hard code
the quiz questions. I will go into more detail about how the detail works in an upcoming part of this tutorial.

The file(s) involved for UI:

    UI/question_text.dart - a stateful widget that displays the question text
    UI/answer_button.dart  - a stateless widget that we use in `QuizPageState` class 
    UI/correct_wrong_overlay.dart - a statefulwidget that we use to display our reaction to user's choice

And the files involved in the logic of the Quiz page are:

    pages/quiz_page.dart - 


TODO
---

stateless widgets vs stateful widgets

animating our widgets


Handling user input
VoidCallback _onTap;

onPressed:
