
[![Build Status](http://img.shields.io/travis/sefakilic/goodreads.svg)](https://travis-ci.org/sefakilic/goodreads)
[![Coverage Status](http://img.shields.io/coveralls/sefakilic/goodreads.svg)](https://coveralls.io/r/sefakilic/goodreads)
[![Documentation Status](https://readthedocs.org/projects/goodreads/badge/?version=latest)](https://readthedocs.org/projects/goodreads/?badge=latest)

# goodreads

This package provides a Python interface for the
[Goodreads API](http://goodreads.com/api). Using it, you can do pretty much
everything that Goodreads allows to do with their own data.

## Dependencies
This package depends on the following packages:

- xmltodict
- requests
- rauth

They can be installed using `pip`.

```
sudo pip install -r requirements.txt
```

If you want to contribute to this package, you will need `nose` package as well.

## Installation

To install, run the following command from the top-level package directory.

```
sudo python setup.py install
```

## Getting Started

The first thing is to request an API key from Goodreads
[here](https://www.goodreads.com/api/keys). Once you have it, you can create a
client instance to query Goodreads.

```python
from goodreads import client
gc = client.GoodreadsClient(<api_key>, <api_secret>)
```

To access some of the methods, you need [OAuth](http://oauth.net/) for
authorization.

```python
gc.authenticate(<access_token>, <access_token_secret>)
```

Note that `access_token` and `access_token_secret` are different from developer
key and secret. For development purposes, you can call the same function with no
parameters to get authorization. It will open a URL pointing
[a Goodreads page](http://goodreads.com) for OAuth permission. For your
application, you can direct the user to that particular URL, ask him/her to
authorize your app and save the returning `access_token` and
`access_token_secret` in your database.

## Examples

This package provides Python interface for most API methods. Here are a few
examples to demonstrate accessing data on Goodreads.

### Books

Let's access the first book added to Goodreads, the book with id 1!

```python
book = gc.book(1)
```

Once you have the `GoodreadsBook` instance for the book, you can access data on
the queried book.

```python
>>> book.title
u'Harry Potter and the Half-Blood Prince (Harry Potter, #6)'
>>> authors = book.authors
>>> authors[0].name
u'J.K. Rowling'
>>> book.average_rating
u'4.49'
```

### Author

You can get information about an author as well.

```python
>>> author = gc.author(2617)
>>> author.name
u'Jonathan Safran Foer'
>>> author.works_count
u'13'
>>> author.books
[Extremely Loud and Incredibly Close, Everything Is Illuminated, Eating Animals, Tree of Codes, Everything is Illuminated & Extremely Loud and Incredibly Close, The unabridged pocketbook of lightning, The Future Dictionary of America, A Convergence of Birds: Original Fiction and Poetry Inspired by Joseph Cornell, New American Haggadah, The Sixth Borough]
```

### User

User data can be retrieved by user id or username.

```python
>>> user = gc.user(1)
>>> user.name
u'Otis Chandler'
>>> user.user_name
u'otis'
>>> user.small_image_url
u'http://d.gr-assets.com/users/1189644957p2/1.jpg'
```

### Group

Let's find a group discussing Python and get more information about it.

```python
>>> g = gc.find_groups("Python")
>>> g = groups[0]
>>> g['title']
u'The Computer Scientists'
>>> group = gc.group(g['id'])
>>> group.description
u'Only for Committed Self Learners and Computer Scientists Who are Starving for
Information, and Want to Advance their Skills Through: Reading, Practicing and
Discussion Computer Science and Programming Books.'
```

### Events

Goodreads API also allows to list events happening in an area.

```python
>>> events = gc.list_events(21229)
>>> event = events[0]
>>> event.title
u'Books and Cocktails'
>>> event.address
u'120 N. Front St.'
>>> event.city
u'Wrightsville'
```

## Contribution

If you find an API method that is not supported by this package, feel free to
create a Github issue. Also, you are  more than welcome to submit a pull request
for a bug fix or additional feature.

## License

[MIT License](http://opensource.org/licenses/mit-license.php)

