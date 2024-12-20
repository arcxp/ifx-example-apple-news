# IFX Example Apple News

Example code is provided by a community of developers. They are intended to help you get started more quickly, but are not guaranteed to cover all scenarios nor are they supported by Arc XP.

> These examples are licensed under the [MIT license](https://mit-license.org/): THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Reiterated from license above, all code in this example is free to use, and as such, there is NO WARRANTY, SLA or SUPPORT for these examples.

----

Get started publishing Arc XP content to Apple News using IFX

Our recipe can be found [here](https://docs.arcxp.com/alc/en/ifx-node-js-recipe-pushing-arc-xp-content-to-apple-news?id=kb_article_view&sys_kb_id=993663ce47a53150eee38788436d4360&spa=1).

## Build Status

![Build Status](https://codebuild.us-east-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiWlhsRUhBTURubTVDeFcrVDljT3NVRHE1bkdxdkZQT2RJbG1TQ0RLaTl0NXJmVkR5QUF6MmJIR3BSaTR4YWZXcUZtalJoQUY2MnRSc0cyZVFqcUVvVGV3PSIsIml2UGFyYW1ldGVyU3BlYyI6IjBhVWo4L0tsL1hkS29pYnQiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=main)

## Building

### Prerequisites

1. Create a personal access token with `read:package` scope in your GitHub account. See ["Creating a personal access token."](https://docs.github.com/en/enterprise-server@3.4/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
2. Once a PAT is created, there are two ways to install the Node.js SDK dependency. The first option is to create your local .npmrc file directly. Another option is to use npm login command.

   - Create your local .npmrc file directly
     ```
     export GITHUB_TOKEN=<your PAT generated through the GitHub console>
     npm config set @arcxp:registry=https://npm.pkg.github.com/
     echo '//npm.pkg.github.com/:_authToken=${GITHUB_TOKEN}' >> ~/.npmrc
     ```
   - Use `npm login`
     ```
     npm login --scope=@arcxp --auth-type=legacy --registry=https://npm.pkg.github.com

     Username: your GitHub username
     Password: your PAT generated through the GitHub console
     Email: your GitHub email
     ```
3. Docker Desktop installed.

### Installation
1. Install NPM packages
   ```
   npm install
   ```
2. Optional: Reset NPM configuration
   ```
   npm config delete @arcxp:registry
   npm logout --registry=https://npm.pkg.github.com/
   ```

## Running

If all succeeded, then you can run:
```
npm run localTestingServer
```

If you want to run the integration locally, then you are required a local dynamoDB, in order to have it you need to install Docker on your machine.

To install Docker on your MacOS you can run the command:
```
brew cask install docker
```

Once you have Docker installed you can test the Docker running the command:
```
docker --version
```

Also make sure you have `docker-compose` installed:
```
docker-compose -v
```

If this is the first time running the integration, configure dummy credentials:
```
aws configure
```

To get started, run:
```
cd localstack
```

Run the following command to start localstack and DynamoDB.

```
docker-compose up
```

To access to the local DynamoDB you'll have to set the following environment variables:
```
AWS_ACCESS_KEY_ID=<your_accessKeyId>
AWS_SECRET_ACCESS_KEY=<your_secretAccessKey>
AWS_DYNAMODB_ENDPOINT=http://localhost:8000
AWS_REGION=us-east-1
```

Note: You can overwrite the default configuration in `localstack/docker-compose.yml`

**Note:** For the **accessKeyId** and the **secretAccessKey** locally the only requirement is contain letters (A–Z, a–z) and numbers (0–9).

## Configuration

### Environment Files

Utilize the `.env.{my-environment}` files in the root directory to provide environment specific
configuration to your application. Do not store secrets or api keys in these files, for those see [Secrets](#secrets)

### Secrets

Secrets are managed via the Arc Admin API. Secrets that you add to your integration via that API get placed as environment variables available to your application on the `process.env` object.

To test secrets while running the local development server, you should create a file called `.env` in
the root directory of your project and store them there. **Note: This file containing secrets should NOT be committed to version control.**

## Deploying

The included example createBundle script will create a zip file from this repo in the bundles directory to deploy to IFX.

### To Create a Bundle

To create a bundle to deploy to sandbox run: `npm run createSandboxBundle`

To create a bundle to deploy to production run: `npm run createProdBundle`

Follow [IFX API](https://dev.arcxp.com/api/integrations/integrations-production/#operations-tag-bundles) documentation for deploying bundles.