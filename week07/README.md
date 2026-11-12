# Week 8
Lambda code:

import json, boto3
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Properties')
def lambda_handler(event, context):
    listing_id = event['pathParameters']['id']
    resp = table.get_item(Key={'L_ListingID': listing_id})
    return {
    'statusCode': 200,
    'body': json.dumps(resp.get('Item', {}))
    }
The path begins with the client making a request, with some HTTP request.
This request hits the API gateway, parsing the request into json to send to the lambda function. The lambda function processes the request, retrieves data from the dynamoDB table. This is returned to API gateway and then the client. 