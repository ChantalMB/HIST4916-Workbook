# HIST4916 Notes: Week 4

- Simple Scraper
  - Running locally in `dhmuse-play` env
  - Have to use `%` instead of `!` to install --> installs into current kernel rather than into the instance of Python that launched the notebook
  - `bs4` lxml parser never installs properly apparently --> have separately installed
  - Kind of in love w bs4 --> simpler than selenium (caveat: can't handle js)
- Building own scraper
  - Found [this cookbook by the Ottawa Gas Co.](https://www.canadiana.ca/view/oocihm.95242/1?r=0&s=1) from the late 19th century -->  course project analyzing cookbooks in Ottawa would be neat
  - Could download PDF of source but would need it in individual images anyway for OCR
    - Image src from HTML:
    ```
    <img id="pvImg" src="https://image-tor.canadiana.ca/iiif/2/oocihm.95242%2Fdata%2Fsip%2Fdata%2Ffiles%2Foocihm.95242.13.jp2/full/!800,800/0/default.jpg?token=eyJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2MTI4MzMyOTcsImRlcml2YXRpdmVGaWxlcyI6Im9vY2lobS45NTI0MlxcL2RhdGFcXC9zaXBcXC9kYXRhXFwvZmlsZXNcXC8uK1xcLihqcGd8anAyfHRpZikiLCJpc3MiOiJDQVAiLCJpYXQiOjE2MTI3NDY4OTd9.q_DDJEQfOOQ9U8jO7bdW8Ezc3-x6N17V5wz6CVOsZXE" alt="Image 13">
    ```
    - That sure is one long access token
  - Going to grab urls for images and generate list of them based on iterator/image number then use `wget` to grab the pictures
    - Note for later: might need to pre-process images a bit before OCR
  - Oh this is less technical than I thought it'd be --> need to iterate at a specific point in the URL so I need the full url in my code and I can't just have it as a variable
    - Copy/pasting from outputted HTML
    - Surely there's a better method than that but I don't know it
  - To make this more informative/specific I'll ID how to isolate the actual image on the page we need
  - `wget` command doesn't work because of the token appended to the end of the URL
    - Phew easy fix by just adding the `--content-disposition` flag
