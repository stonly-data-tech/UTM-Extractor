# UTM-Extractor

This script is used to process events in order to extract and add the `utm_source`, `utm_medium`, `utm_campaign`, `utm_content` and `utm_term` properties from the `current_url`, `$current_url`, `signUpPageConversion`, `signUpPageLanding`, `firstPageViewed` properties of an event.

The script exports a single function, `processEvent(event, { config })`, which takes in two arguments:

    event: the event object that needs to be processed
    config: an object containing any configuration options that may be required by the script

The `processEvent()` function first checks if the event object has a properties field, and if it does, it iterates through the urlProperties array, checking if the event object has any of the properties in the array that includes the string 'utm'. If it does, it then iterates through the `utmProperties` array, and uses `extractUtmFromUrl(urlString, utm)` to extract the value of the utm properties from the URL. If the value is not empty, it adds the extracted value to the event object's properties field.

The `extractUtmFromUrl(urlString, utm)` function takes the `urlString` and utm as input and it uses the URL class from the built-in url module to create a new URL object, and uses the `searchParams.get(utm)` method to get the value of the utm parameter from the url.

Finally, the processed event object is returned by the `processEvent()` function, to be ingested by the system that called it.

The extracted URL utm  properties are then add to the event object, before they are ingested into a data pipeline your analytics platform. This is useful for tracking the source of the user's visit to the website.