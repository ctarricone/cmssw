# Using edmTracerCompactLogViewer.py

## Introduction
The `edmTracerCompactLogViewer.py` is used to create a human understandable representation of the file generated by the `Tracer` service. Two representations are possible: text and interactive web.

## Creating Tracer file
To create a Tracer file, add the following to a cmsRun configuration
```python
process.add_(cms.Service("Tracer",
                         useMessageLogger=cms.untracked.bool(False)),
                         fileName=cms.untracked.string("<name of file>"))
```
Where `"<name of file>"` is whatever name you want to use for the file that will hold the Tracer output. The use of `useMessageLogger=cms.untracked.bool(False)` is optional but does
help avoid creating a large output from cmsRun.

## Processing Tracer file
The Tracer file can either be processed to output a human readable text output (similar to what the Tracer service does when `useMessageLogger==True`) or create a `data.js` file that
can be used by a web application.

### text output
Issue the shell command
```edmTracerCompactLogViewer.py <name of file>```

The script will output to the screen the text output. It is probably most useful to redirect the output to a file.

If you only want to see the framework transitions and not all the information about ED or ES modules, you can use the option `-f`.

### web output
Issue the shell command
```edmTracerCompactLogViewer.py -w <name of file>```

The script will outut a new file named `data.js`.

If you only want to see the framework transitions and not all the information about ED or ES modules, you can use the option `-f`.

#### setup web data

You will need to copy all the files in `$CMSSW_RELEASE_BASE/src/FWCore/Services/web` to a directory you can access from a web browser. Copy the `data.js` file
created by `edmTracerCompactLogViewer.py` into that same web browser accessible directory. Now you can have your web browser access the `index.html` file.

For directions on how to use the web application, see the [`FWCore/Services/web/README.md`](../web/README.md) file.
