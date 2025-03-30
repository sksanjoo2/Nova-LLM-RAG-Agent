llm-bedrock
PyPI Changelog Tests License

Run prompts against models hosted on AWS Bedrock

Installation
Install this plugin in the same environment as LLM.

llm install llm-bedrock
Credentials
You'll need an access key and a secret key to use this plugin, with permission granted to access the Bedrock Nova models.

If you have already configured the AWS CLI on your machine you may be able to skip this step, as the plugin will automatically use the credentials from the CLI.

You still need to request access to the Bedrock models in the AWS console, which should be provisioned automatically within seconds of you filing the request.

If you want to use the plugin with dedicated IAM credentials (an access key and a secret key) follow these step by step instructions by Nils Durner.

Combine those into a access_key:secret_key format (joined by a colon) and paste that into:

llm keys set bedrock
# paste access_key:secret_key here
Usage
Run llm models to see the list of models. The Amazon Nova models are:

us.amazon.nova-micro-v1:0 (alias: nova-micro) - cheapest and fastest, text only
us.amazon.nova-lite-v1:0 (alias: nova-lite) - can handle text, images and PDFs
us.amazon.nova-pro-v1:0 (alias: nova-pro) - can handle text, images and PDFs, best and most expensive
Run a prompt like this:

llm -m nova-pro 'a happy poem about a pelican with a secret'
Images and videos and PDFs can be provided using the -a option, which takes a file path or a URL:

llm -m nova-lite 'describe this image' -a https://static.simonwillison.net/static/2024/pelicans.jpg
If you want to use Bedrock in a region other than the default one (us-west-2), set your AWS_REGION environment variable, e.g.

export AWS_REGION=eu-west-1
Development
To set up this plugin locally, first checkout the code. Then create a new virtual environment:

cd llm-bedrock
python -m venv venv
source venv/bin/activate
Now install the dependencies and test dependencies:

llm install -e '.[test]'
To run the tests:

python -m pytest
To regenerate the captured HTTP responses:

PYTEST_BEDROCK_API_KEY="$(llm keys get bedrock)" python -m pytest --record-mode all
