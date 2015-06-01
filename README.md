# PNG Diff
Small PNG diff utility, written in pure JS for Node.

```bash
npm install png-diff
```

## Usage

(_Check out the example folder._)

Both methods take two image paths/streams/buffers as input.

```js
var fs = require('fs');
var PNGDiff = require('png-diff');

var image2Stream = fs.createReadStream('2.png');
PNGDiff.outputDiff('1.png', image2Stream, 'diffOutput.png', function(err, diffMetric) {
  if (err) throw err;
  // returns 0 if every pixel's the same; return 1 otherwise.
  console.log(diffMetric !== 0 ? 'Difference detected.' : 'No difference');
  // highlights the difference in red
  console.log('Diff saved!');
});

var image1Buffer = fs.createReadStream('1.png');
PNGDiff.outputDiffStream(image1Buffer, '2.png', function(err, outputStream, diffMetric) {
  if (err) throw err;

  if (diffMetric === 0) {
    console.log('No difference, no need to output diff result.');
    return;
  }
  outputStream.pipe(fs.createWriteStream('diffOutput2.png'));
});
```

All credits go to @chenglou for releasing https://www.npmjs.com/package/png-diff
I've only changed the diffMetric output.

## License
MIT.
