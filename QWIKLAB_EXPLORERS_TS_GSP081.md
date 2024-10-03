# Cloud Functions: Qwik Start - Console || [GSP081](https://www.cloudskillsboost.google/focuses/1763?parent=catalog) ||

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

### Run the following Commands in CloudShell
```
export REGION=
```
```
gcloud services enable run.googleapis.com

sleep 10

mkdir Awesome && cd Awesome

cat > index.js <<EOF_END
/**
 * Responds to any HTTP request.
 *
 * @param {!express:Request} req HTTP request context.
 * @param {!express:Response} res HTTP response context.
 */
exports.GCFunction = (req, res) => {
    let message = req.query.message || req.body.message || 'Hey There !';
    res.status(200).send(message);
  };
  
EOF_END


cat > package.json <<EOF_END
{
    "name": "sample-http",
    "version": "0.0.1"
  }
  
EOF_END


gsutil mb -p $DEVSHELL_PROJECT_ID gs://$DEVSHELL_PROJECT_ID

export PROJECT_NUMBER=$(gcloud projects describe $DEVSHELL_PROJECT_ID --format="json(projectNumber)" --quiet | jq -r '.projectNumber')

sleep 30

# Set the service account email
SERVICE_ACCOUNT="service-$PROJECT_NUMBER@gcf-admin-robot.iam.gserviceaccount.com"

# Get the current IAM policy
IAM_POLICY=$(gcloud projects get-iam-policy $DEVSHELL_PROJECT_ID --format=json)

# Check if the binding exists
if [[ "$IAM_POLICY" == *"$SERVICE_ACCOUNT"* && "$IAM_POLICY" == *"roles/artifactregistry.reader"* ]]; then
  echo "IAM binding exists for service account: $SERVICE_ACCOUNT with role roles/artifactregistry.reader"
else
  echo "IAM binding does not exist for service account: $SERVICE_ACCOUNT with role roles/artifactregistry.reader"
  
  # Create the IAM binding
  gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
    --member=serviceAccount:$SERVICE_ACCOUNT \
    --role=roles/artifactregistry.reader

  echo "IAM binding created for service account: $SERVICE_ACCOUNT with role roles/artifactregistry.reader"
fi

echo "${GREEN}${BOLD}If "${RED}${BOLD}ERROR${RESET}", ignore it${RESET}"

gcloud functions deploy GCFunction \
  --region=$REGION \
  --gen2 \
  --trigger-http \
  --runtime=nodejs20 \
  --allow-unauthenticated \
  --max-instances=5

echo "${GREEN}${BOLD}If "${RED}${BOLD}ERROR${RESET}", ignore it${RESET}"

DATA=$(printf 'Nice to Meet You !' | base64) && gcloud functions call GCFunction --region=$REGION --data '{"data":"'$DATA'"}'

sleep 60

sleep 30

export PROJECT_NUMBER=$(gcloud projects describe $DEVSHELL_PROJECT_ID --format="json(projectNumber)" --quiet | jq -r '.projectNumber')

# Set the service account email
SERVICE_ACCOUNT="service-$PROJECT_NUMBER@gcf-admin-robot.iam.gserviceaccount.com"

# Get the current IAM policy
IAM_POLICY=$(gcloud projects get-iam-policy $DEVSHELL_PROJECT_ID --format=json)

# Check if the binding exists
if [[ "$IAM_POLICY" == *"$SERVICE_ACCOUNT"* && "$IAM_POLICY" == *"roles/artifactregistry.reader"* ]]; then
  echo "IAM binding exists for service account: $SERVICE_ACCOUNT with role roles/artifactregistry.reader"
else
  echo "IAM binding does not exist for service account: $SERVICE_ACCOUNT with role roles/artifactregistry.reader"
  
  # Create the IAM binding
  gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
    --member=serviceAccount:$SERVICE_ACCOUNT \
    --role=roles/artifactregistry.reader

  echo "IAM binding created for service account: $SERVICE_ACCOUNT with role roles/artifactregistry.reader"
fi


gcloud functions deploy GCFunction \
  --region=$REGION \
  --gen2 \
  --trigger-http \
  --runtime=nodejs20 \
  --allow-unauthenticated \
  --max-instances=5


DATA=$(printf 'Stay Cool' | base64) && gcloud functions call GCFunction --region=$REGION --data '{"data":"'$DATA'"}'
```

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)
