# Twilio SMS Plus

A library to send SMS messages with Twilio *plus* some added functionality such as:

* Converting phone number to E164 format
* Logging all SMS messages to an AWS S3 bucket

## Installation

```shell
npm install --save twilio-ssm-plus
```

## Usage

Example usage:

```javascript
const toPhoneNumber = '6095551212'
const params = {
  textMessage: 'hello world!',
  toPhoneNumber: toPhoneNumber,
  fromPhoneNumber: '2125551212',
  logS3bucket: 'twilio-logs-dev',
  logS3keyPrefix: `users/${toPhoneNumber}/transcript`
}

const twilioPlus = new TwilioSmsPlus({
  twilioAccountSide: process.env.TWILIO_ACCOUNT_SID,
  twilioAuthToken: process.env.TWILIO_AUTH_TOKEN
})
const result = await twilioPlus.sendTextMessage(params)
```

## Testing

The tests require the following SSM parameters to exist in the AWS account:

```
/fpw/TWILIO_ACCOUNT_SID
/fpw/TWILIO_AUTH_TOKEN
/fpw/TWILIO_FROM_NUMBER
/fpw/TWILIO_TEST_TO_NUMBER
```

test.sh requires an argument with the name of the AWS profile used for credentials.  The test script in package.json indicates a profile named "fpwdev", but this can be changed as:

```shell
$ chmod +x ./test.sh
$ ./test.sh myprofilenamehere
```

## License

MIT
