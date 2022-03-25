
# Data generation

The simulated datasets are based on the [Librispeech](http://www.openslr.org/12) corpus and the [100 Nonspeech Sounds](http://web.cse.ohio-state.edu/pnl/corpus/HuNonspeech/HuCorpus.html) corpus.

**Update 2021.06.16:** It is observed that several utterances might encounter clipping when saving the waveforms to files. Since this is also a possible case in real-world communications, I do not force then to be clipped but instead add an optional choice to avoid clipping or not in the generation script.

**Update 2019.11.10:** The configuration files and the data generation script have been updated. Please make sure you are using the most recent files for data generation.

## Raw data download

1) Download the *train-clean-100*, *dev-clean* and *test-clean* data from Librispeech's website and unzip them into any directory. The absolute path for the directory is denoted as *libri_path*, which should contain 3 subfolders *train-clean-100*, *dev-clean* and *test-clean*.
2) Download the 100 Nonspeech Sounds data and unzip it into any directory. The absolute path for the directory is denoted as *noise_path*.
3) Download or clone this repository.

## Additional Python packages

- [soundfile](https://pypi.org/project/SoundFile/)==0.10.0
- [gpuRIR](https://github.com/DavidDiazGuerra/gpuRIR) (it does not provide version information, but the latest build should be fine)

## Dataset generation

run `python create_dataset.py --output-path=your_output_path --avoid-clipping=0 --dataset='adhoc' --libri-path=libri_path --noise-path=noise_path`, where:
1) *output_path*: the absolute path for saving the output. Default is empty which uses the current directory as output path.
2) *avoid_clipping*: whether to avoid clipping when saving the waveforms to files. 0 (default): keep the original scale. 1: avoid clipping.
3) *dataset*: the dataset to generate. It can only be *'adhoc'* or *'fixed'*.
4) *libri_path*: the absolute path for Librispeech data.
5) *noise_path*: the absolute path for noise data.
