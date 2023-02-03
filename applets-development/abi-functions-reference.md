# ABI Functions Reference

### Host functions

Below is the list of functions exported by the W3bstream VM that you can import into your WASM module to access functionalities provided by the W3bstream host.

<pre class="language-go"><code class="lang-go"><strong>/**
</strong> * Get event data.
 *
 * Provides access to the buffer of data attached to W3bstream event 
 *
 * @param resource_id the event id, provided by W3bstream in the _start function.
 * @param return_ptr pointer to the data buffer
 * @param return_size the size in bytes of the data buffer
 * @return 0 if no errors.
 */
fn ws_get_data(resource_id i32, return_ptr i32, return_size i32) -> i32 

/**
 * Set event data.
 *
 * Inject modified event data back in the source event for further processing
 * @Notice: This is not used yet
 *
 * @param resource_id the event id, provided by W3bstream in the _start function.
 * @param ptr pointer to the data buffer
 * @size the size in bytes of the data buffer
 * @return 0 if no errors.
*/
fn ws_set_data(resource_id i32, ptr i32, size i32) -> i32 

/**
 * Read data from DB
 *
 * Get a serialized object from the W3bstream database at a specific key.
 * 
 * @param namespace_data the namespace name (depends on the DB config)
 * @param namespace_size the length of the namespace string
 * @param key_data the key you want to fetch from the DB
 * @param key_size the length of the key string
 * @param return_value_ptr is the pointer to the fetched DB data
 * @param return_value_size the size of fetched DB data
 * @return 0 if there are no errors.
*/
fn ws_get_db(namespace_data i32, namespace_size i32, key_data i32, key_size i32,
    return_value_ptr i32, return_value_size i32) -> i32 

/**
 * Store data in DB
 *
 * Store a serialized object in the W3bstream database at a specific key.
 * 
 * @param namespace_data the namespace name (depends on the DB config)
 * @param namespace_size the length of the namespace string
 * @param key_data the key you want to store the data under in the DB
 * @param key_size the length of the key string
 * @param value_ptr is the pointer to the data to store
 * @param value_size the size of the data
 * @return 0 if there are no errors.
*/
fn ws_set_db(namespace_data i32, namespace_size i32, key_data i32, key_size i32,
    value_ptr i32, value_size i32) -> i32 

/**
 * Log a message
 *
 * Log a string to the W3bstream console
 * 
 * @param log_level The log level (Trace = 1, Debug, Info, Warn, Error) 
 * @param ptr The pointer to the string to be logged
 * @param size the length of the string
 * @param key_data the key you want to fetch from the DB
 * @return 0 if no errors.
*/
fn ws_log(log_level i32, ptr i32, size i32) -> i32 

/**
 * Send a blockchain transaction
 *
 * Sends a transaction to the blockchain network that has been 
 * configured on the host side. 
 * 
 * @param ptr The pointer to the stringified transaction data
 * @param size the length of the data
 * @return 0 if no errors.
*/
fn ws_send_tx(ptr i32, size: i32) -> i32;

/**
 * Call a contract function
 *
 * Calls a (view or pure) contract function on the blockchain network  
 * configured on the host side. 
 * 
 * @param ptr The pointer to the stringified transaction data
 * @param size the length of the data
 * @return 0 if no errors.
*/
fn ws_call_contract(ptr i32, size: i32, return_ptr i32, return_size i32 ) -> i32;

</code></pre>

### Applet functions

Below is the list of functions that your WASM module is required to export to the W3bstream host:

<pre class="language-rust"><code class="lang-rust">// Provide an implementation unless already provided by the WASM compiler you're using
<strong>fn malloc(size: usize) -> *mut c_void 
</strong>
// Default handler called by W3bstream upon a new event
fn _start(resource_id i32) -> i32 
</code></pre>
