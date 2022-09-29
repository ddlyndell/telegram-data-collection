## Overview

It connects to Telegram's API. It generates JSON files containing channel's data, including channel's information and posts. You can search for a specific channel, or a set of channels provided in a text file (one channel per line.)

Files are saved by default in a folder called *output/data*. These folders are created by the script.

```
├──🗂 Telegram-api
|   └──main.py
|   └──🗂 config
|   	└──config.ini
|   └──🗂 output
|   	└──collected_chats.csv
|   	└──🗂 data
|   		└──file_messages.json
|   		└──channel.json
|   		└──etc.
```

### Options

* `--telegram-channel` Specifies Telegram Channel to download data from.
* `--batch-file` File containing Telegram Channels to download data from, one channel per line.
* `--limit-download-to-channel-metadata` Will collect channels metadata only, not channel's messages. (default = False)
* `--min-id` Specifies the offset id. This will update Telegram data with new posts.


**Examples**

### Basic request

```
python main.py --telegram-channel channelname`
```

**Expected output**

- Excel file of collected channels
- JSON file containing channel's profile metadata
- JSON file containing posts from the requested channel

<br />

### Request using a text file containing a set of channels

```
python main.py --batch-file './path/to/channels_text_file.txt'
```

**Expected output**

- Excel file of collected channels
- JSON files containing channels' profile metadata
- JSON files containing posts from each requested channel

These examples will retrieve all posts available through the API from the requested channel. If you want to collect channel's information only, without posts, you can run:

### Limit download to channel's metadata only

```
python main.py --telegram-channel channelname --limit-download-to-channel-metadata
```

or, using a set of telegram channels via a text file:

```
python main.py --batch-file './path/to/channels_text_file.txt' --limit-download-to-channel-metadata
```

### Updating channel's data

If you want to collect new messages from one channel, you need to identify the message ID from the last post. Once you identify the id, run:

```
python main.py --telegram-channel channelname --min-id 12345
```

**Expected output**

- Excel file of collected channels - based on new messages
- JSON file containing channel's profile metadata
- JSON file containing new messages posted after the requested ID (min ID)

---

## build-datasets.py

```
python build-datasets.py
```

This Python script reads the collected files and creates a new dataset containing messages from the requested channels. By default, the created dataset in CSV format will be located in the `output` folder.

```
├──🗂 Telegram-api
|   └──main.py
|   └──🗂 output
|   	└──msgs_dataset.csv
```

---

## channels-to-network.py

```
python channels-to-network.py
```

This Python script builds a network graph. By default, the file will be located in the `output` folder. The script also shows a preliminary graph using the modules matplotlib, networkx, and python-louvain, which implements community detection. You can use import the graph file in different softwares, including Gephi.

```
├──🗂 Telegram-api
|   └──main.py
|   └──🗂 output
|   	└──Graph.gexf
```

---
