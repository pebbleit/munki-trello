# Introduction

This is a script that utilises a Trello board to manage the promotion of Munki items through development to testing to production catalogs. 

# Usage

## Setup

It's recommended that this script is run under a service Trello account rather than a real persons, so you can separate the changes made by the script from normal users. This user will need to have access to the Trello board you're using. You will need to know the board ID - the board ID is the part after ``/b`` and before the name of your board (https://trello.com/b/_AbCdEfGh_/my-trello-board)

You will need an [API key](https://trello.com/app-key). Make note of the key and then head over to [Trello's instructions](https://trello.com/docs/gettingstarted/#token) for creating a user token. Choose how long you want to issue to token for - using the value of 'never' will stop the token from expiring. The only required option is read and write access to the Trello account. The name can be anything you like, it's how you will identify the token in future.

```
https://trello.com/1/authorize?key=substitutewithyourapplicationkey&name=munki-trello&expiration=never&response_type=token&scope=read,write
```

You will be given a 64 character string that you will need to take note of.

## Running the script

You have two options - you can run the script manually on a machine with the Munki Tools installed (this will run on OS X or Linux, Windows isn't tested), or you can use the Docker container. For more details about the Docker container, see it's own repository.

### Example

```
$ python munki-trello.py --boardid 12345 --key myverylongkey --token myevenlongertoken

# Troubleshooting

> I'm seeing items that won't move to the next stage no matter how often I move them.

Make sure the combination of ``name`` and ``version`` is unique. For speed, the initial ingest of Munki data is done via your ``all`` catalog rather than traversing your pkgsinfo files. O=If you have two pkgsinfo files that have the same version / name combination as anther, this script won't touch anything after the first. Once the duplicate(s) have been removed, the item will be promoted to the next stage.