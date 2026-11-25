# Speech Recogniser

Speech to text for Ghanaian Pidgin, Twi and English, small enough to run offline on a phone. Started September 2026.

Work in progress. The training code and model weights aren't published here yet.

## Why

My phone understands my English and gives up the moment I switch to Pidgin or Twi, which in Accra is most sentences. The open models that handle Twi are over 2 GB, far too big for a phone.

## What I did

I measured Whisper base (74 million parameters) on 300 clips in each language. It got most of the English right and almost none of the Twi. For Twi I trained on the WAXAL and Ghana NLP speech datasets. There was no Ghanaian Pidgin speech dataset, so I recorded one: 11 hours from 40 classmates and friends, transcribed by hand. A 2.4 GB Twi model transcribed hours of Twi radio, and the small model learned from its answers. Every transcript starts with a language tag (`<gpe>`, `<tw>` or `<en>`), so one model handles all three languages and says which one it heard.

The first version wrote every Pidgin sentence as "corrected" English: "I dey go" came out as "I they go". English outnumbered Pidgin 40 to 1 in the training data. Balancing every batch across the three languages, and spelling Pidgin the way people type it on WhatsApp, fixed most of it.

## Result

- 19% word error rate on Ghanaian Pidgin, down from 71%.
- 41 MB on the phone after 8-bit quantisation.
- Runs offline and writes out ten seconds of speech in about two seconds.

## Next

I'm recording more Ghanaian Pidgin, aiming for 50 hours by March 2027, and I plan to release the recordings as an open dataset.

## Tools

Python and PyTorch with Hugging Face Transformers, trained on free Kaggle GPUs and exported to ONNX for the phone.

## Data

- [WAXAL](https://huggingface.co/datasets/google/WaxalNLP), collected by Google with the University of Ghana and others (CC BY 4.0).
- [Ghana NLP speech corpus](https://huggingface.co/datasets/ghananlpcommunity/ghana-speech) (CC BY-NC 4.0).

More at [ernestbaffour.com](https://ernestbaffour.com/#speech).
