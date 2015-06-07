# Pyrebase

A simple python interface for the Firebase REST API.

## Installation

pip install pyrebase

## Usage

### Initialising your Firebase

```
ref = pyrebase.Firebase('https://yourfirebaseurl.firebaseio.com', 'yourfirebasesecret')
```

### Saving Data

#### POST

To save data with an autogenerated, unique, timestamp-based key, use the POST method.
Example of an autogenerated key: -JqSjGteC4SRzNJ2hH52

```
data = '{"name": "Marty Mcfly", "date_created": "05-11-1955"}'
post_this = ref.post("articles", data, None)
```

#### PUT

To create your own keys you can use the PUT method. The key in the example below is "Marty".

```
data = '{"Marty": {"name": "Marty Mcfly", "date_created":"05-11-1955"}}'
put_this = ref.put("users", data, None)
```

### Reading Data

There are four methods for retrieving data with Pyrebase: all, sort_by, sort_by_first, and sort_by_last.

#### all

All takes a child and an optional callback function, returning all data under the child.

```
def my_callback():
    print("Working while we wait...")

gimme_all = ref.all("users", my_callback())
```

#### sort_by

Sort_by takes a child, category, and optional callback function, returning data sorted by category.

```
my_users = ref.sort_by("users", "name", None)
```

#### sort_by_first

Sort_by_first takes a child, category, start_at, limit_to_first, and optional callback.

start_at finds the first instance of that value in the category.
limit_to_first restricts the amount of data returned.

```
sort_first = ref.sort_by_first("articles", "index", 5, 10, None)
```
Here we search for data in "articles" and sort them by "index". We start sorting from an article with an index value
of 5, and limit our results to 10 results. If all of our articles had indexes incremented by 1, we would retrieve a
sorted list starting with an