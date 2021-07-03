# localstack-hello-world

localstack-hello-world - https://localstack.cloud

## setup

```sh
/usr/bin/python3 -m pip install --upgrade pip
pip install localstack
pip install --upgrade localstack localstack-ext localstack-client
docker pull localstack/localstack
```

## start

```sh
localstack start
or
docker-compose up
```

```sh
aws --endpoint-url=http://localhost:4566 iam create-role --role-name lambda-ex --assume-role-policy-document '{"Version": "2012-10-17","Statement": [{ "Effect": "Allow", "Principal": {"Service": "lambda.amazonaws.com"}, "Action": "sts:AssumeRole"}]}'

aws --endpoint-url=http://localhost:4566 iam attach-role-policy --role-name lambda-ex --policy-arn arn:aws:iam::aws:policy/service-role/AWSLambdaBasicExecutionRole

aws --endpoint-url=http://localhost:4566 lambda create-function --function-name my-math-function --zip-file fileb://my-deployment-package.zip --handler lambda_function.lambda_handler --runtime python3.8 --role arn:aws:iam::000000000000:role/lambda-ex

aws --endpoint-url=http://localhost:4566 lambda invoke \
  --function-name my-math-function \
      --cli-binary-format raw-in-base64-out \
          --payload '{"action": "square","number": 3}' output.txt
```
