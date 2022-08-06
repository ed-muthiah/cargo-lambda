<script setup>
const platform = (navigator.platform || '').toLowerCase();
const win = platform.includes('win');
const mac = platform.includes('mac');
const linux = platform.includes('linux');
</script>

# Getting Started

This section will help you build a Rust function for AWS Lambda from scratch. If you already have an existent function, and would like to build it for AWS Lambda, start from Step 4.

## Step 1: Install Cargo Lambda

<div v-if="win">
You can use <a href="https://scoop.sh/">Scoop</a> to install Cargo Lambda on Windows. Run the following commands to add our bucket, and install it:

```sh
scoop bucket add cargo-lambda https://github.com/cargo-lambda/scoop-cargo-lambda
scoop install cargo-lambda/cargo-lambda
```
</div>

<div v-if="mac">
You can use <a href="https://brew.sh/">Homebrew</a> to install Cargo Lambda on MacOS and Linux. Run the following commands on your terminal to add our tap, and install it:

```sh
brew tap cargo-lambda/cargo-lambda
brew install cargo-lambda
```
</div>

<div v-if="linux">
You can use <a href="https://pypi.org/">PyPI</a> to install Cargo Lambda on Linux:

```sh
pip3 install cargo-lambda
```
</div>

See all the ways that you can use to [install Cargo Lambda](/guide/installation) in your system.

## Step 2: Create a new project

The [new](/commands/new) subcommand will help you create a new project with a default template. When that's done, change into the new directory:

```sh
cargo lambda new new-lambda-project \
    && cd new-lambda-project
```

::: tip
Add the flag `--http-feature apigw_rest` if you want to automatically generate an HTTP function that integrates with Amazon API Gateway
:::

## Step 3: Serve the function locally for testing

Run the Lambda emulator built in with the [watch](/commands/watch) subcommand:

```sh
cargo lambda watch
```

## Step 4: Test your function

The [invoke](/commands/invoke) subcommand can send payloads to the function running locally:

```sh
cargo lambda invoke --data-ascii '{"command": "hi"}'
```

If you're testing an HTTP function, you can access it with your browser from the local endpoint: [localhost:9000/lambda-url/new-lambda-project](localhost:9000/lambda-url/new-lambda-project).

## Step 5: Build the function to deploy it on AWS Lambda

Use the [build](/commands/build) subcommand to compile your function for Linux systems:

```sh
cargo lambda build --release
```

::: tip
Add the flag `--arm64` if you want to use Gravitron processors on AWS Lambda
:::

## Step 6: Deploy the function on AWS Lambda

Use the [deploy](/commands/deploy) subcommand to upload your function to AWS Lambda. This subcommand requires AWS credentials in your system, and an IAM role with basic Lambda privileges:

```sh
cargo lambda deploy --iam-role FULL_ROLE_ARN
```

## Debugging

Use the flag `--verbose` with any subcommand to enable tracing instrumentation. You can also enable instrumentation with the following environment variable `RUST_LOG=cargo_lambda=trace`.

## Rust version

This project works with Rust 1.59 and above.