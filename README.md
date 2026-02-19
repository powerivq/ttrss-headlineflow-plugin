# TT-RSS Headline Flow Plugin

Plugin for [Tiny Tiny RSS](http://tt-rss.org), a web-based news feed reader and aggregator.

## Project Lineage

This repository is a fork of:
https://github.com/hrk/tt-rss-newsplus-plugin/tree/master

This project is a newer successor to News+.

## What It Adds

The plugin adds custom API methods used by [Headline Flow](http://github.com/noinnion/headlineflow/) for synchronization and feed management:

- `headlineflowGetCompactHeadlines`
- `headlineflowUpdateCategory`
- `headlineflowAddCategory`
- `headlineflowRemoveCategory`
- `headlineflowUpdateFeedCategory`

## Compatibility

- Requires Tiny Tiny RSS 1.8 or newer.
- Plugin directory name: `api_headlineflow`
- System plugin name to enable: `api_headlineflow`

## Installation

1. Clone this repository (or download and extract it) into your TT-RSS `plugins/` directory.
2. Confirm you have `plugins/api_headlineflow/`.

## Configuration

### Single User

1. Log in to your TT-RSS instance.
2. Open Preferences.
3. Scroll to plugins and enable `api_headlineflow` (listed under system plugins).

### All Users

Edit `config.php` and add `api_headlineflow` to the list of system plugins so it is enabled for every user.

## API Reference

### `headlineflowGetCompactHeadlines`

Returns a JSON-encoded list of headline IDs matching the input parameters.

Parameters:

- `feed_id` (integer/string): Only output articles for this feed (see feed ID notes below).
- `limit` (integer): Limits the number of returned articles.
- `skip` (integer): Skips this number of articles first.
- `view_mode` (string): One of `all_articles`, `unread`, `adaptive`, `marked`, `updated`.
- `since_id` (integer): Only returns articles with an ID greater than this value.

Notes:

- `limit`: Unlike the standard `getHeadlines` API call, there is no hardcoded limit. Default is `20`.
- `feed_id`: Values between `-10` and `0` have special meanings:
  - `0`: archived
  - `-1`: starred
  - `-2`: published
  - `-3`: fresh
  - `-4`: all articles
  - `-6`: recently read
  - IDs `< -10`: labels
  - Textual `feed_id`: browsing by tags

### `headlineflowUpdateCategory`

Updates an existing feed category.

Parameters:

- `category_id` (integer): Existing category ID.
- `title` (string): New category title.
- `parent_category_id` (integer, optional): New parent category ID. Use `0` for root.

### `headlineflowAddCategory`

Creates a feed category.

Parameters:

- `title` (string): Category title.
- `parent_category_id` (integer, optional): Parent category ID. Use `0` for root.

### `headlineflowRemoveCategory`

Removes an existing feed category.

Parameters:

- `category_id` (integer): Existing category ID.

### `headlineflowUpdateFeedCategory`

Updates category assignment for an existing feed.

Parameters:

- `feed_id` (integer): Existing feed ID.
- `category_id` (integer): Target category ID. Use `0` to move the feed to uncategorized.

## License

This code is licensed under GPLv3 and inherits the same license as TT-RSS source code it was built upon.
