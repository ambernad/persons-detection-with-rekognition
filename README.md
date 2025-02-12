# Solution for persons detection from survelliance camera screenshots

<H1>Architecture</H1>
<img width="758" alt="image" src="https://github.com/user-attachments/assets/49239597-0c95-4705-8b49-16048f6232fd" />

<H1>How to deploy</H1>
1. Create Cloudformation stack using ABR-Rekognition-CF-v2.yaml. In stack parameters specify unique suffix to ensure that your resources will have unique names
</br>
2. Launch the Stack and wait until it succesfully completed
</br>
3. Go to S3 bucket abr-screenshots-${RandomSuffix}. Go to bucket properties. Create Event notification. 
</br>Set unique name for notification
</br>Set checkbox for Event type - All object create events
</br>Set destination - Lambda function and pick abr-process-screenshots-${RandomSuffix} function from drop-down list
</br>
4. Go to lambda functions. Replace in the lambda code abr-screenshots-${RandomSuffix} and abr-results-${RandomSuffix}  with real bucket names
</br>
5. Put your screenshot to abr-screenshots-${RandomSuffix} bucket using console or API. Check that result reports are created in abr-results-${RandomSuffix} bucket
</br>
6. Go to Glue Crawler abr-results-crawler-${RandomSuffix} and run crawling proccess. Alternatively you can put the crawler on schedule, for example, every hour.
</br>
7. After crawling completion go Athena. Select abr-surveillance-db-${RandomSuffix} database and launch query on abr-results-${RandomSuffix} table

