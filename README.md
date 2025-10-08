# Prerequisites 
Before a content supplier can use the ST Digital Distribution API, they must obtain access to ST Digital's AWS S3 bucket to upload their content.


# Folder Structore / Order of placement
- Batch Folder (YYYYMMDDHHmmsssnnn)
  1. Audio File (.wav)
  2. Cover Photo (.jpg)
  3. Metadata File (manifest.json)

*The `manifest.json` file should be placed at the end of the upload process, as it serves as the trigger to initiate content ingestion into our system.*
  
![alt text](https://kb.ddex.net/images/a749ea36830b7bd07b6add0590c0ba83.png)


# Metadata File Structure
``` json
{ 
  "title": "Release Title",
  "upc": "12 digit UPC",
  "genre": "Release Genre",
  "subgenre": "Release Subgenre",
  "label": "Label Name",
  "physicalReleaseDate": "Physical Release Date",
  "storeReleaseDate": "Store Release Date",
  "cline": "© Line",
  "productionYear": "Production Year",
  "catalogueNumber": "Catalogue Number",
  "coverPhoto": "cover photo file name with extenction",
  "tracks": [{
    "title": "Track Title",
    "isrc":"ISRC code",
    "primaryArtist":[
      {
        "name": "Primary Artist Name",
        "spotifyId": "Primary Artist Spotify ID",
        "youtubeId": "Primary Artist Youtube ID"
      }
    ],
    "writers":["Writer 1", "Writer 2"],
    "composers":["Composer 1", "Composer 2"],
    "musicDirectors":["Music Director 1", "Music Director 2"],
    "producers":["Producer 1", "Producer 2"],
    "publisher":"Publisher Name",
    "language":"Language",
    "youtubeUrl":"Youtube URL",
    "lyrics":"Lyrics",
    "media":"Audio file name with extenction"
  }]
}
```

---

- title *`Required, maxLength: 150`*
- upc *`Optional, If present, should be unique acress all the releases, type: String, length: 12`*
- genre *`Required, Find the availabel genres below`*
- subgenre *`Required, Find the available genres below, should be associated with the genre field`*
- label *`Required, maxLength: 70, If an associated label with your account already exists in our database, it will be used; otherwise, a new label will be created.`*
- physicalReleaseDate *`Required, format: YYYY-MM-DD`*
- storeReleaseDate *`Required, format: YYYY-MM-DD`*
- cline *`Required, Should not be same as release title, maxLength: 300`*
- productionYear *`Required, format: YYYY, type: String`*
- catalogueNumber *`Required, format: alphanumeric, maxLength: 20`*
- coverPhoto *`Required, Cover photo file name: any_name.jpg, dimension: 3000x3000`*
- tracks.title *`Required, maxLength: 150`*
- tracks.isrc *`Optional, If present, should be unique acress all the tracks, format:QZZ432375885`*
- tracks.primaryArtist: *`Required, Array of primaryArtist with name,spotifyId and youtubeId, only name is required`*
- tracks.writers: *`Required, Array of string`*
- tracks.composers: *`Optional, Array of string`*
- tracks.musicDirectors: *`Required, Array of string`*
- tracks.producers: *`Required, Array of string`*
- tracks.publisher: *`Required, maxLength: 70`*
- tracks.language: *`Required, Find the availabel languages below`*
- tracks.youtubeUrl: *`Required, Must be a youtube video url`*
- tracks.lyrics: *`Optional, maxLength:3000`*
- tracks.media: *`Required, Audio file name: any_name.wav, acceptedFormat:.wav, maxFileSize: 800mb`*

## Points to remember
- Each release must have a unique batch folder.
- If a release contains multiple tracks, upload all tracks within the same batch folder.
- The metadata file should contain accurate and up-to-date information.

> Resources

| Genre | Subgenre | 
| ----------- | ----------- |
| Childrens Music | Hip-Hop, Lullabies, Nursery Rhymes, Pop Songs |
| Christian & Gospel | Christian Metal, Christian Pop, Christian Rap, Christian Roc, Classic Christian, Contemporary Gospel, Gospel, Praise & Worship, Southern Gospel, Traditional Gospel |
| Indian | Children Song, Classical / Instrumental, Devotional & Spiritual, Devotional & Spiritual - Aarti, Devotional & Spiritual - Bhajan, Devotional & Spiritual - Chhath Geet, Devotional & Spiritual - Ganesh Bhajan, Devotional & Spiritual - Hanuman Bhajan, Devotional & Spiritual - Krishan Bhajan, Devotional & Spiritual - Mantras, Devotional & Spiritual - Mata Bhajan, Devotional & Spiritual - Patriotic Song, Devotional & Spiritual - Ram Bhajan, Devotional & Spiritual - Sai Bhajan, Devotional & Spiritual - Shabad Gurbani, Devotional & Spiritual - Shiv Bhajan, Gazal, Hindustani Classical, Indian - Assamese, Indian - Awadhi, Indian - Bengali, Indian - Bhojpuri, Indian - Bollywood, Indian - Classical, Indian - DJ, Indian - Fusion, Indian - Gujarati, Indian - Haryanvi, Indian - Himachali, Indian - Hindi, Indian - Holi Geet, Indian - Islamic, Indian - Kannada, Indian - Kashmiri, Indian - Khortha, Indian - Maithili, Indian - Manipuri, Indian - Marathi, Indian - Nagpuri, Indian - Odia, Indian - Pahari, Indian - Punjabi, Indian - Punjabi Pop, Indian - Rajasthani, Indian - Sambalpuri, Indian - Santali, Indian - Tamil, Indian - Telugu, Indian Folk, Indian Pop, Indian-Adivasis Song, Indian-Awadhi, Indian-Cg Song, Indian-Dehati Rasiya, Indian-Dehati Song, Indian-Karbi Song, Indian-Maghi, Indian-Patriotic, Regional India, Sufi, Traditional, Urdu |
| World | Country, Country - Pop, Dance, Dance - DJ Mix, Dance - Trance, Easy Listening, Hip Hop, Instrumental, Jazz, Latin, Pop, R&B, Reggae, Rock, World, World - Chinese - Classical, World - Chinese - Flute, World - Chinese - Opera, World - Chinese - Regional Folk, World - Chinese - Strings, World - Chinese - Taiwanese Folk, World - Chinese - Tibetan Native Music, World - Devotional & Spiritual, World - Devotional & Spiritual - Islamic, World - India, World - India - Bollywood, World - India - Ghazals, World - India - Indian Classical, World - India - Indian Folk, World - India - Indian Pop, World - India - Punjabi Pop, World - India - Regional Indian, World - India - Tamil, World - India - Telugu, World - Nepali, World - Pakistan - Dari, World - Pakistan - Khowar, World - Pakistan - Pashto, World - Pakistan - Shina, World - Thai |

| Lanugages |
| ----------- |
| Adivasis, Arabic, Assamese, Awadhi, Bengali, Bhojpuri, Chhattisgarhi, Chinese, Dari, Dogri, English, Gujarati, Haryanvi, Himachali, Hindi, Indonesian, Kannada, Karbi, Kashmiri, Khortha, Khowar, Korean, Maghi, Maithili, Malayalam, Manipuri, Marathi, Nagpuri, Nepali, Oriya, Pahari, Pashto, Plains Karbi, Punjabi, Rajasthani, Sanskrit, Santali, Shina, Sindhi, Spanish, Tamil, Telugu, Thai, Urdu, Vietnamese |

