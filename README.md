# Q-Fetcher

Congrats, you are about to implement an highly sophisticated service, whose sole purpuse is - gathering students questions from various sources.

### Requirements:
* The service should fetch academic questions, which are provided in several data formats. results required to be processed and returned to fetcher. 

* The predefined URLs for the different data sources are specified at manifest file located: [S3_BUCKET_MANIFEST_URL]. 
each line stands as questions data source. 

* Data Sources:

    * **Image**
Question's text can be easily extracted via "Google Cloud Vision API" OCR capebilities.
You can either utilize [GCloud SDK](https://cloud.google.com/vision/docs/detecting-text) in prefered language or use following REST API endpoint:

        ```json
        POST https://vision.googleapis.com/v1/images:annotate?key=[API_KEY]
        {
            "requests": [
                {
                    "image": {
                        "content": "/9j/7QBEUGhvdG9zaG9...base64-encoded-image-content...fXNWzvDEeYxxxzj/Coa6Bax//Z"
                    },
                    "features": [
                        {
                        "type": "TEXT_DETECTION"
                        }
                    ]
                }
            ]
        }
        ```


    * **JSON**
        The relevant field to process is *"text"*. 
        Note that result can return more than single question.
        ```json
        {
            "questions": [
                {
                    "id": 1,
                    "text": "To be or not to be?",
                    "field": "literature"
                }
            ...
            ]
        }
        ```

    * **CSV**
        ```
        id,text,field
        1, Among 150 math students 42 have taken Discrete Math, 32 have taken History of Math. There are 12 have taken both. (a.) How many students have take only Discrete Math, but not History of Math? (b.) How many students have taken only History of Math, but not Discrete Math?,math
        2, Which life history is exemplified by an organism that produces many offspring, but doesn't invest in the care of the offspring allowing the organism to take advantage of favorable conditions? (a) equilibrial life history (b) maturation life history (c) predictable life history (d) opportunistic life history, biology
        ```


* Data should be parsed, aggregated and combined into single textual json response.
```json
{
    "questions": [{
        "value": "To be or not to be?",
        "source": "json"
    },
    ...
    ]
}
```
* Service should be tolerante to response delays and return aggregated response within a reasonable time (e.g. max 30 secs)
* Make sure your code is easily extensible for any future data endpoints, easy to understand for future developers, and beautiful!

### Important

* Feel free implementing with your prefered language & frameworks - node.js, python, java, c#
* You are encouraged to use any 3rd party library that you like working with, i.e. express

### Bonus

We love to see some UI! Add some basic web rendering to display results and whatever you feel fits.
