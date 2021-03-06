# ncli

this is a WIP CLI app to send data to [nomie](https://nomie.app/).

you will only need node and npm.

## setup

```bash
$ cd
$ git clone https://github.com/mxtetrachord/nc ~/.ncli
$ cd .ncli
$ npm i && npm build
$ echo 'alias ncli="node $HOME/.ncli/build/index.js"' >> ~/.bash_profile
```

## usage

all you need to bring to nomie is your config file. we've included a stub in `/src/config.example.json` you can follow. (you should rename that file to `config.json`.) your config file needs two things:

- `apiKey: string`: this can be found in nomie's [api settings](https://open.nomie.app/api) page.
- `options: (string | boolean)[][]`: an array of arrays. example:

```bash
[
  // cli flag, nomie tracker name, range of values
  ["m", "#mood", "1..5"],
  ["e", "#energy", "1..10"],
  // pass `true` as your final param to use one-tap trackers.
  ["c", "#coffee", true],
]
```

with the above options, you can call 

```bash
$ ncli -m 1 -e 8 -c
```

which will hydrate into `#mood(1), #energy(8), #coffee(1)`.

you'll be given an opportunity to make sure your data is correct. here's a typical `ncli` run:

```bash
λ ncli -m 1 -e 2 -c

here's what we heard.
  #mood(1)
  #energy(2)
  #coffee

should we log this to nomie? Y/n
y
```

## interactive mode
calling  `ncli -i`  starts "interactive mode"; we'll step through all your range options one-by-one and ask you for your response. then we'll scoop up all that data, let you review it all, and send it to nomie. (note: we won't ask about one-tap trackers here.) here's an example run in interactive mode:

```bash
λ ncli -i

starting interviewer...

how is your #mood? 1
how is your #energy? 2

here's what we heard.
  #mood(1)
  #energy(2)

should we log this to nomie? Y/n
y
```
