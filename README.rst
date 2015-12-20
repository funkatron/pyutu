pyutu
-----
.. image:: https://img.shields.io/pypi/v/pyutu.svg
   :target: https://pypi.python.org/pypi/pyutu

.. image:: https://img.shields.io/pypi/dm/pyutu.svg
   :target: https://pypi.python.org/pypi/pyutu

.. image:: https://secure.travis-ci.org/lashex/pyutu.png?branch=master
   :target: http://travis-ci.org/lashex/pyutu

A Python-based CLI and library for cloud pricing APIs. Currently covering `AWS Pricing <http://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/price-changes.html>`_.

  **utu** from the Maori_ language, can be a verb that means to repay, pay, ...
.. _Maori: http://maoridictionary.co.nz/word/8937

  **pyutu** – if said fast, sounds like "pay you too" ... which seems appropriate.

Initially, this library just strives to simplify pulling product details and pricing terms from a Service's Offer File for a given Region.

(early) Examples
================
.. code-block:: bash

  $ pyutu index
  Publication Date: 2015-12-09T23:40:29Z
  Format Version: v1.0
  Offers: {'AmazonVPC': {'offerCode': 'AmazonVPC', 'currentVersionUrl': '/offers/v1.0/aws/AmazonVPC/current/index.json'}, ...snip...
  ...snip...

.. code-block:: javascript

  $ pyutu price ddb
  Service Alias: AmazonDynamoDB
            URL: https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/AmazonDynamoDB/current/index.json
         Region: us-west-2
         Prices: {
    "55NFVN8W7N8G6PPF": {
      "offerCode": "AmazonDynamoDB",
      "product": {
        "attributes": {
          "fromLocation": "US West (Oregon)",
          "fromLocationType": "AWS Region",
          "operation": "",
          "servicecode": "AWSDataTransfer",
          "toLocation": "US West (N. California)",
          "toLocationType": "AWS Region",
          "transferType": "InterRegion Inbound",
          "usagetype": "USW2-USW1-AWS-In-Bytes"
        },
        "productFamily": "Data Transfer",
        "sku": "55NFVN8W7N8G6PPF"
      },
      "term": {
        "55NFVN8W7N8G6PPF.JRTCKXETXF": {
          "effectiveDate": "2015-07-01T00:00:00Z",
          "offerTermCode": "JRTCKXETXF",
          "priceDimensions": {
            "55NFVN8W7N8G6PPF.JRTCKXETXF.6YS6EN2CT7": {
              "appliesTo": [],
              "beginRange": "0",
              "description": "$0.00 per GB - US West (Oregon) data transfer from US West (Northern California)",
              "endRange": "Inf",
              "pricePerUnit": {
                "USD": "0.0000000000"
              },
              "rateCode": "55NFVN8W7N8G6PPF.JRTCKXETXF.6YS6EN2CT7",
              "unit": "GB"
            }
          },
          "sku": "55NFVN8W7N8G6PPF",
          "termAttributes": {}
        }
      }
    },
    "5FP5929JZN6XVXN5": {
    ...snip...

.. code-block:: javascript

  $ pyutu --region=us-west-1 price s3
  Service Alias: AmazonS3
            URL: https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/AmazonS3/current/index.json
         Region: us-west-1
         Prices: {
    "2DM84SHX9TG8MVBG": {
      "offerCode": "AmazonS3",
      "product": {
        "attributes": {
          "fromLocation": "US West (N. California)",
          "fromLocationType": "AWS Region",
          "operation": "",
          "servicecode": "AWSDataTransfer",
          "toLocation": "South America (Sao Paulo)",
          "toLocationType": "AWS Region",
          "transferType": "InterRegion Inbound",
          "usagetype": "USW1-SAE1-AWS-In-Bytes"
        },
        "productFamily": "Data Transfer",
        "sku": "2DM84SHX9TG8MVBG"
      },
      "term": {
        "2DM84SHX9TG8MVBG.JRTCKXETXF": {
          "effectiveDate": "2015-10-01T00:00:00Z",
          "offerTermCode": "JRTCKXETXF",
          "priceDimensions": {
            "2DM84SHX9TG8MVBG.JRTCKXETXF.6YS6EN2CT7": {
              "appliesTo": [],
              "beginRange": "0",
              "description": "$0.00 per GB - US West (Northern California) data transfer from South America (Sao Paulo)",
              "endRange": "Inf",
              "pricePerUnit": {
                "USD": "0.0000000000"
              },
              "rateCode": "2DM84SHX9TG8MVBG.JRTCKXETXF.6YS6EN2CT7",
              "unit": "GB"
            }
          },
          "sku": "2DM84SHX9TG8MVBG",
          "termAttributes": {}
        }
      }
    },
    "3B9GTFM3KPQRE6VR": {
    ...snip...


TODOs
=====
- [ ] Add more product filtering criteria: OnDemand or Reserved
- [ ] Given a service and a partial or full SKU, get prices
- [ ] Add ability to find products by arbitrary attributes: EC2 'storage', 'memory', etc.
- [ ] Add ability to find specific product families' prices