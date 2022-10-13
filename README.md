# API Development and Documentation Final Project

## Trivia App

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a webpage to manage the trivia app and play the game, but their API experience is limited and still needs to be built out.

That's where you come in! Help them finish the trivia app so they can start holding trivia and seeing who's the most knowledgeable of the bunch. The application must:

1. Display questions - both all questions and by category. Questions should show the question, category and difficulty rating by default and can show/hide the answer.
2. Delete questions.
3. Add questions and require that they include question and answer text.
4. Search for questions based on a text query string.
5. Play the quiz game, randomizing either all questions or within a specific category.

Completing this trivia app will give you the ability to structure plan, implement, and test an API - skills essential for enabling your future applications to communicate with others.

## Starting and Submitting the Project

[Fork](https://help.github.com/en/articles/fork-a-repo) the project repository and [clone](https://help.github.com/en/articles/cloning-a-repository) your forked repository to your machine. Work on the project locally and make sure to push all your changes to the remote repository before submitting the link to your repository in the Classroom.

## About the Stack

We started the full stack application for you. It is designed with some key functional areas:

### Backend

The [backend](./backend/README.md) directory contains a partially completed Flask and SQLAlchemy server. You will work primarily in `__init__.py` to define your endpoints and can reference models.py for DB and SQLAlchemy setup. These are the files you'd want to edit in the backend:

1. `backend/flaskr/__init__.py`
2. `backend/test_flaskr.py`

> View the [Backend README](./backend/README.md) for more details.

### Frontend

The [frontend](./frontend/README.md) directory contains a complete React frontend to consume the data from the Flask server. If you have prior experience building a frontend application, you should feel free to edit the endpoints as you see fit for the backend you design. If you do not have prior experience building a frontend application, you should read through the frontend code before starting and make notes regarding:

1. What are the end points and HTTP methods the frontend is expecting to consume?
2. How are the requests from the frontend formatted? Are they expecting certain parameters or payloads?

Pay special attention to what data the frontend is expecting from each API response to help guide how you format your API. The places where you may change the frontend behavior, and where you should be looking for the above information, are marked with `TODO`. These are the files you'd want to edit in the frontend:

1. `frontend/src/components/QuestionView.js`
2. `frontend/src/components/FormView.js`
3. `frontend/src/components/QuizView.js`

By making notes ahead of time, you will practice the core skill of being able to read and understand code and will have a simple plan to follow to build out the endpoints of your backend API.

> View the [Frontend README](./frontend/README.md) for more details.

### Endpoints Documentation

#### GET /questions
- General:
    . Returns a list of all questions, all categories of questions, success values and total number of questions
    . Questions are paginated in groups of 10. Include a request argument to choose page number, starting from 1
- Sample: `curl http://localhost:5000/question`

```
{
    "categories":
    {
        "1":"Science",
        "2":"Art",
        "3":"Geography",
        "4":"History",
        "5":"Entertainment",
        "6":"Sports"
    },
    "questions":
        [
            {
                "answer":"Edward Scissorhands",
                "category":5,
                "difficulty":3,
                "id":6,
                "question":"What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
            },
            {
                "answer":"Muhammad Ali",
                "category":4,
                "difficulty":1,
                "id":9,
                "question":"What boxer's original name is Cassius Clay?"
            },
            {
                "answer":"Brazil",
                "category":6,
                "difficulty":3,
                "id":10,
                "question":"Which is the only team to play in every soccer World Cup tournament?"
            },
            {
                "answer":"Uruguay",
                "category":6,
                "difficulty":4,
                "id":11,
                "question":"Which country won the first ever soccer World Cup in 1930?"
            },
            {
                "answer":"George Washington Carver",
                "category":4,
                "difficulty":2,
                "id":12,
                "question":"Who invented Peanut Butter?"
            },
            {
                "answer":"Lake Victoria",
                "category":3,
                "difficulty":2,
                "id":13,
                "question":"What is the largest lake in Africa?"
            },
            {
                "answer":"The Palace of Versailles",
                "category":3,
                "difficulty":3,
                "id":14,
                "question":"In which royal palace would you find the Hall of Mirrors?"
            },
            {
                "answer":"Agra",
                "category":3,
                "difficulty":2,
                "id":15,
                "question":"The Taj Mahal is located in which Indian city?"
            },
            {
                "answer":"Escher",
                "category":2,
                "difficulty":1,
                "id":16,
                "question":"Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
            },
            {
                "answer":"Mona Lisa",
                "category":2,
                "difficulty":3,
                "id":17,
                "question":"La Giaconda is better known as what?"
            }
        ],
    "success":true,
    "totalQuestions":19
}
```
#### GET /categories
- General:
    . Returns a list of all categories, success value and total number of categories
- Sample: `curl http://localhost:5000/categorie`

```
{
    "categories":
        {
            "1":"Science",
            "2":"Art",
            "3":"Geography",
            "4":"History",
            "5":"Entertainment",
            "6":"Sports"
        },
        "success":true,
        "total_categories":6
}
```

#### DELETE /questions/{questions_id}
- General:
    . Deletes the question of the given ID if it exists. Returns the ID of the deleted question, success value and a status cde of 200
- Sample: `curl -X DELETE http://localhost:5000/questions/`

```
{
    "deleted": 6,
    "status_code":200,
    "success":true
}
```

#### POST /questions
- General:
    . Creates a new question using the submitted question, answer, difficulty and category. Return the id of the created question and a success value
- Sample: `curl -X POST -H "Content-Type: application/json" -d '{"question": "newquestion", "answer": "new answer", "difficulty": "1", "category": "1"}' http://localhost:5000/questions'`

```
{
    "created":192,
    "success":true
}
```

#### POST /questions/search
- General:
    . Return questions based on a search term. Also return the success value, current category and the total of questions found
- Sample: `curl -X POST -H"Content-Type: application/json" -d '{"searchTerm": "1930"}'http://localhost:5000/questions/search`

```
{
    "current_category":null,
    "questions":
        [
            {
                "answer":"Uruguay",
                "category":6,
                "difficulty":4,
                "id":11,
                "question":"Which country won the first ever soccer World Cup in 1930?"
            }
        ],
    "success":true,
    "total_questions":1
}
```

#### GET /categories/{id}/questions
- General:
    . Return questions based on the category ID, success value, current category and the total of questions found if the category exists
- Sample: `curl http://localhost:5000/categories/1/question`

```
{
    "currentCategory":1,
    "questions":
        [
            {
                "answer":"The Liver",
                "category":1,
                "difficulty":4,
                "id":20,
                "question":"What is the heaviest organ in the human body?"
            },
            {
                "answer":"Alexander Fleming",
                "category":1,
                "difficulty":3,
                "id":21,
                "question":"Who discovered penicillin?"
            },
            {
                "answer":"Blood",
                "category":1,
                "difficulty":4,
                "id":22,
                "question":"Hematology is a branch of medicine involving the study of what?"
            },
        ],
        "success":true,
        "totalQuestions":3
}
```

#### POST /quizzes
- General:
    . Return a set of random question based on choosen category and success value. If you choose All category, it returns a set of random question with no specific category
    . Questions are diplayed one by one and don't repeat
- Sample for a given category: `curl -X POST -H "Content-Type: application/json" -d {"previous_questions": [], "quiz_category": {"id": "1", "type": "Science"}}' http://localhost:5000/quizzes`

```
{
    "question":
        {
            "answer":"Blood",
            "category":1,
            "difficulty":4,
            "id":22,
            "question":"Hematology is a branch of medicine involving the study of what?"
        },
    "success":true
}
```

- Sample for all category: `curl -X POST -H "Content-Type: application/json" -d {"previous_questions": [], "quiz_category": {"id": "0", "type": "click"}}' http://localhost:5000/quizzes`

```
{
    "question":
        {
            "answer":"One",
            "category":2,
            "difficulty":4,
            "id":18,
            "question":"How many paintings did Van Gogh sell in his lifetime?"
        },
    "success":true
}
```

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "error":500,
    "message":"Server error",
    "success":false
}
```

The API will return five error types when request fail:
- 400: Bad request
- 404: Not found
- 405: Method not allowed
- 422: Unprocessable
- 500: Server error
