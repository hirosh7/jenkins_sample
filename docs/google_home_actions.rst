Creating a new Google Home Action
=================================
Details for this exercise are pulled from Dialogflow's `Building Your First Agent
<https://dialogflow.com/docs/getting-started/building-your-first-agent/>`_ tutorial.

The goal of the exercise is to create a new Google Home action that let's a user know when Southern California Edison's
energy periods are (e.g. on-peak, off-peak, super off-peak).

Start with signing up for an `api.ai account <https://dialogflow.com/>`_ (i.e. Dialogflow.com now). I signed in with my
regular Google account. After getting to the dialogflow dashboard, I noticed that there's a **'Setup Google Assistant
Integration'** option not mentioned in the tutorial. I clicked on the option and was asked to create a project. These
projects seem to be associated with project created on Google's Cloud Compute platform. I selected the option to create
a new project and got the following response back

.. code:: bash

   Agent was successfully linked to Google Project myagent-cdee4

Not sure where I'll use this but it's set up just in case. First we'll start with the tutorial's weather app to get
a feel for the workflow.

1) Create a new agent by clicking on the **Create Agent** option
2) Create Intents. You are automatically put into this dialog after your agent is created.I populated the intents
   with the default training phrases specified in the tutorial. Note how adding training phrases with dates or city
   names will automatically insert general purpose parameters (e.g. @sys.date or @sys.geo-city) which can be used to
   generalize commands to use, in this case, any date or any city name
3) In the top right of the page, there's a **'Try it Now'** dialog. You can now type in a phrase to test your action.
   This is very cool. If you use a date or city in your test phrase, it's automatically identified as such. Of course,
   you don't get a reponse back yet, as none have been programmed.
4) Now we add responses to the intents. The responses are canned and not very flexible which is why it's necessary
   (in this case) to set up **fulfillment** so the intent can call an API and return relevant weather information and
   make sure the conversation doesn't go off the rails.

Fulfillment involves setting up your server to connect via command line to the Google Cloud Platform environment. The
details can be found in the tutorial's `Before You Begin <https://cloud.google.com/functions/docs/quickstart>`_  link
in the tutorial's **Setup Google Cloud Project** section. I ran through all those steps (connecting to the
**my-weather** GCP project. This process also involved installing the Google Cloud SDK so that we can successfully run
GCP commands from the server terminal command line.

Next step was to copy the sample Node.js code into a file, save it and deploy it

.. code:: bash

   # After creating a project directory and saving the Node.js index.js file, make sure you run the
   # following commands from that project directory (e.g. ~/sandbox/google_weather)
   gcloud beta functions deploy helloHttp --stage-bucket staging.my-weather-49339.appspot.com --trigger-http

.. note::
   --stage-bucket [BUCKET_NAME] can be found by going to your related `Google Cloud project
   <https://console.cloud.google.com/home/dashboard?project=my-weather-49339>`_ and clicking
   on Cloud Storage under the Resources section

That command yielded the following output

.. code:: bash

    Created .gcloudignore file. See `gcloud topic gcloudignore` for details.
    Deploying function (may take a while - up to 2 minutes)...done.
    availableMemoryMb: 256
    entryPoint: helloHttp
    httpsTrigger:
      url: https://us-central1-my-weather-49339.cloudfunctions.net/helloHttp
    labels:
      deployment-tool: cli-gcloud
    name: projects/my-weather-49339/locations/us-central1/functions/helloHttp
    serviceAccountEmail: my-weather-49339@appspot.gserviceaccount.com
    sourceArchiveUrl: gs://staging.my-weather-49339.appspot.com/us-central1-projects/my-weather-49339/locations/us-central1/functions/helloHttp-ofdeiobapupy.zip
    status: ACTIVE
    timeout: 60s
    updateTime: '2018-04-30T00:43:30Z'
    versionId: '1'

You can now copy and paste the **httpsTrigger URL** above into your browser and see the output specified in the
sample Node.js index.js file.













