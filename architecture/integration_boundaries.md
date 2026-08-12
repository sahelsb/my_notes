

### How should I depend on someone else's code


1. Dependency (in-process). You `uv add` it and import it. Its code runs inside your process, in
	  your call stack. You inherit its dependency tree and version constraints. No network.

	```bash
	u add "simple-eval @ git+ssh://git@gitlab.ancud.de:2222/data-    
	science/awa/simple_eval.git@eb1746d"
	```

  3. HTTP call (out-of-process). It runs as its own process; you send JSON over a socket. Two
	  flavours, same category:
  - raw — `httpx.post(url, json=...) `at the call site
  - client module — a small local wrapper holding the base URL, timeout, auth, error mapping, one function per endpoint

	  A vendor SDK (stripe, openai) is also this category: pip-installed, but it contains only
	  wire-protocol code, not the server. So "installed as a dependency" and "called over HTTP" aren't opposites.

  3. Protocol client. Same as #2, but the protocol has standardized discovery, so one generic client
	  works against any server —` MultiServerMCPClient` calls get_tools() and learns the tool list at runtime. No hand-written endpoint mapping.



|Ask|Answer →|
|---|---|
|Does it own state or a running process?|**yes → HTTP** · **no → dependency**|
|Is it the system under test, or your measuring apparatus?|**under test → HTTP** (measure it as deployed) · **apparatus → dependency**|
|What do you pass it?|**JSON payloads → HTTP** · **Python objects, callables → dependency**|
|Would running it as a service be absurd?|**yes → dependency**|


**Cost of a dependency**: you inherit its deps and pins. 
**Cost of HTTP**: serialization, a process to boot, no type checking across the boundary.


##### Example

```bash
integra → HTTP. It's a service: owns the sqlite DB, runs as integra-api / integra-mcp, exists whether or not you do. It's also the system under test, and the real production client (MaiselApi.ts in the BFF) reaches it over HTTP — so your harness must too, or you're grading a code path nobody runs.
  

simple_eval → dependency. It's a library: graders.py, evaluator.py, models.py — pure functions and pydantic types, nothing running, no port to call. It's your measuring apparatus, not the thing measured. You'll hand it Case objects and grading functions, which don't survive a JSON round-trip. "POST /grade, body: my grader function" is absurd.  
  
```