`TrainingSpeech` is an initiative to provide **open and freely reusable dataset** of voices 

 - for speech-to-text models training

 - on non-english languages 

 - using already available data (such as audio-books).
 

Right now, data are extracted exclusively from audio-books and in French language. Let me know if you are intersted to contribute [by creating an issue](https://github.com/nicolaspanel/TrainingSpeech/issues/new).



## Tooling

`TrainingSpeech`  comes with a CLI that automate and simplify:
 - transcript extraction
 - [forced-alignment](https://github.com/pettarin/forced-alignment-tools#definition-of-forced-alignment) (using [aeneas](https://github.com/readbeyond/aeneas))
 - validation and correction



## Common workflow

### 1. Generate and validate alignment on existing source

1. pick a source that have NOT been validated yet: see `python manage.py stats` and `./sources.json` for more info
2. download assets (ie epub and mp3 files): `python manage.py download -s <SOURCE_NAME>`
3. check alignment: `python manage.py check-alignment <SOURCE_NAME>` (may require multiple iterations)
4. send a pull request with generated transcript and alignment

### 2. Add New source (team members only)

1. retrieve epub and corresponding mp3 file and store them into `./data/epubs` and `./data/mp3` (respectively)
2. create new source into `./sources.json` (NB: all fields are mandatory)
3. generate initial transcript using `python manage.py build-transcript <SOURCE_NAME>`
4. upload epub and mp3 files on S3 `python manage.py upload -s <SOURCE_NAME>`


## Dev setup 

```sh
$ sudo apt-get install -y ffmpeg espeak libespeak-dev python3-numpy python-numpy libncurses-dev libncursesw5-dev sox libsqlite3-dev
$ git clone git@github.com:wasertech/TrainingSpeech.git
$ pip3 install --user pipenv
$ cd TrainingSpeech
$ pipenv install --python=3.6.6
$ pipenv sync
$ pipenv shell
$ pytest
```


## Last releases & download
Releases are ready-to-use `zip` archives containing :
 - short 16kHz 16bit wav audio speeches (0-15s)
 - a single `data.csv` file with following columns:
   - `path`: path to the audio file inside the archive
   - `duration`: audio duration in second
   - `text`: transcript


| Name                                                                                                    |   # speeches |   # speakers | Total Duration | Language   |
|:--------------------------------------------------------------------------------------------------------|-------------:|-------------:|:---------------|:-----------|
| [2019-04-11_fr_FR](https://drive.infomaniak.com/app/share/327683/85ec2469-8a64-4a8a-8de0-43e262d32d38/16/download) (w/ 💖 from [@lissyx](https://github.com/lissyx)) |        67577 |            4 | 95:27:21       | fr_FR      |
