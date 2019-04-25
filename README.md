# Tracium

*Tracium* is a [Google Lighthouse](https://github.com/GoogleChrome/lighthouse)
tracing parser extracted into a stand-alone library.

This is a modern version similar to [Big Rig](https://github.com/googlearchive/node-big-rig).

## Usage

Install:
```
$ npm install tracium
```

Example:

```js
const Tracium = require('tracium');
const traceJSON = JSON.parse(fs.readFileSynt('./mytrace.json'));
const tasks = Tracium.computeMainThreadTasks(traceJSON, {
  // |flatten| default to |false|. When false, only top-level tasks will be returned.
  flatten: true,
});
```

## API

#### tracium.computeMainThreadTasks(traceJson[, options])
- `traceJson` <[Object]> A JSON of a Chromium trace
- `options` <[Object]>  Set of options for trace processing
  - `flatten` <[boolean]> Defaults to `false`. Whether to flatten tasks tree. 
- returns: <[Array]<[Object]>> An array of tasks:
  - `kind` <[string]> describes task attribution. Can be one of the following:
    - `'praseHTML'`
    - `'styleLayout'`
    - `'paintCompositeRender'`
    - `'scriptParseCompile'`
    - `'scriptEvaluation'`
    - `'garbageCollection'`
    - `'other'`
  - `startTime` <[number]> monotonic start time in milliseconds
  - `endTime` <[number]> monotonic end time in milliseconds
  - `duration` <[number]> task duration in milliseconds, a.k.a. "wall time"
  - `selfTime` <[number]> time spent in the task at the current level of the task tree
  - `event` <[Object]> original trace event object associated with the task
  - `children` <[Array<[Task]>> an array of child tasks
  - `parent` <?[Task]|> a parent task if any

If `flatten` is passed to `false`, than only top-level tasks will be returned.

<details>
<summary>An example task</summary>

```
{
  event:
   { pid: 29772,
     tid: 775,
     ts: 588826692280,
     ph: 'X',
     cat: 'toplevel',
     name: 'TaskQueueManager::ProcessTaskFromWorkQueue',
     args:
      { src_file: '../../base/trace_event/trace_log.cc',
        src_func: 'SetEnabled' },
     dur: 27,
     tdur: 22,
     tts: 514358 },
  startTime: 0,
  endTime: 0.027,
  children: [],
  duration: 0.027,
  selfTime: 0.027,
  kind: 'other' }
```
</details>

[Array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array "Array"
[boolean]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type "Boolean"
[Buffer]: https://nodejs.org/api/buffer.html#buffer_class_buffer "Buffer"
[function]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function "Function"
[number]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type "Number"
[Object]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object "Object"
[origin]: https://developer.mozilla.org/en-US/docs/Glossary/Origin "Origin"
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise "Promise"
[string]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type "String"
[stream.Readable]: https://nodejs.org/api/stream.html#stream_class_stream_readable "stream.Readable"
[Error]: https://nodejs.org/api/errors.html#errors_class_error "Error"
[ChildProcess]: https://nodejs.org/api/child_process.html "ChildProcess"
[iterator]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols "Iterator"
[Element]: https://developer.mozilla.org/en-US/docs/Web/API/element "Element"
[Map]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map "Map"
[selector]: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors "selector"
[Serializable]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#Description "Serializable"
[xpath]: https://developer.mozilla.org/en-US/docs/Web/XPath "xpath"
[UnixTime]: https://en.wikipedia.org/wiki/Unix_time "Unix Time"