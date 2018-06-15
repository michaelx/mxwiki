## Start a session

```sh
screen -S sessionname
```

## List all sessions

```sh
screen -list
```

or

```sh
screen -ls
```

## Close session

To close a session type `ctrl + d` while inside the session.

To close a session while not connected to it:

```sh
screen -X -S [#session you want to kill] quit
```

## Connect to session

```sh
screen -r -d [#session]
```

## Dettach session

Detached means the user left the screen session running, but disconnected from it. To dettach from a session type `ctrl + a` followed by `d`.