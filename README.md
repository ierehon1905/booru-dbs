# booru-dbs

Collection of different scans from booru sites

## Favorites table (gelbooru)

Around 2818 unique users and around 999717 unique posts. Around 2100134 ratings in total.

|     | item_id | user_id |
| --- | ------- | ------- |
| 0   | 7146390 | 1       |
| 1   | 7136712 | 1       |
| 2   | 7132254 | 1       |
| 3   | 6994042 | 1       |
| 4   | 6951571 | 1       |

## Full database

Full database with posts, tags, users and favorites was too big for github so I had to use Google Drive.

https://drive.google.com/file/d/19zedU0OR_1oGH-K9H4G2WJmjOXcn5VVp/view?usp=sharing

### Tables

| Table   | Primary key          | Foreign key          | Columns                                                                                                                                                                                                                                                                                                                                                     |
| ------- | -------------------- | -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `users` | `user_id`            |                      | `user_id`                                                                                                                                                                                                                                                                                                                                                   |
| `favs`  | `user_id`, `post_id` | `user_id`, `post_id` | `user_id`, `post_id`                                                                                                                                                                                                                                                                                                                                        |
| `posts` | `id`                 |                      | `id`, `created_at`, `score`, `width`, `height`, `md5`, `directory`, `image`, `rating`, `source`, `change`, `owner`, `creator_id`, `parent_id`, `sample`, `preview_height`, `preview_width`, `tags`, `title`, `has_notes`, `has_comments`, `file_url`, `preview_url`, `sample_url`, `sample_height`, `sample_width`, `status`, `post_locked`, `has_children` |

### Utils

The date in `created_at` column is in specific format so in order to parse it I used something like this:

```python
from dateutil.parser import parse as parse_date
from datetime import datetime

parsed_data = parse_date(x)

# For example find age in seconds

diff_sec = (datetime.now().astimezone() - parse_date(x)).total_seconds()
```

For properly parsing the tags I used something like this:

```python
import html

tag_list = html.unescape(x).split(' ')
```
