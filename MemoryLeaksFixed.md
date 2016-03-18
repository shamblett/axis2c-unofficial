### Changesets where that errors is fixed ###

You can review our fixes in changesets:
  * [ce488696ddad](https://code.google.com/p/axis2c-unofficial/source/detail?r=ce488696ddad591674e0ca1feb65aa9200c18a52);
  * [182d1ac5d29b](https://code.google.com/p/axis2c-unofficial/source/detail?r=182d1ac5d29bc96caa741071db5ad8b3a79e3131) (see `*`.c files);
  * [2b0363594d69](https://code.google.com/p/axis2c-unofficial/source/detail?r=2b0363594d69af964e9752ffbbb79b10f2402b2f);
  * [ab057e4ceb47](https://code.google.com/p/axis2c-unofficial/source/detail?r=ab057e4ceb4758c166c2fac0a10386701e035748).
  * [5434bb0a55d0](https://code.google.com/p/axis2c-unofficial/source/detail?r=36a4dcc1140b73347326db3842a501b2f5942e4a)

### List of memory errors fixed ###

| **originator**                          | **description** |
|:----------------------------------------|:----------------|
| http\_transport\_utils.c:1421           | `engine` in HEAD metod is not freed |
| http\_transport\_utils.c:1494           | `engine` in GET metod is not freed |
| http\_transport\_utils.c:1572           | `engine` in DELETE metod is not freed |
| http\_transport\_utils.c:1605           | `query_str` is not freed |
| http\_transport\_utils.c:1800           | freeing of statically allocated `tmp2` may cause memory corruption |
| http\_transport\_utils.c:1824`*`        | `tmp2` is not freed |
| http\_transport\_utils.c:1829`*`        | `tmp2` is not freed |
| http\_transport\_utils.c:1831`*`        | `tmp2` is not freed |
| http\_transport\_utils.c:1836`*`        | `tmp2` is not freed |
| http\_transport\_utils.c:1840`*`        | `tmp2` is not freed |
| http\_transport\_utils.c:1878`*`        | `tmp2` is not freed |
| http\_transport\_utils.c:1909`*`        | `tmp2` is not freed, copy-paste leak: instead of `ret` there must be `tmp2` |
| http\_transport\_utils.c:1915`*`        | `tmp2` is not freed |
| http\_transport\_utils.c:1917`*`        | `tmp2` is not freed |
| http\_transport\_utils.c:1977           | `axutil_hash_index_t hi` won't free doing to break operator. |
| http\_transport\_utils.c:1992           | `content` remain allocated also if file was not opened |
| http\_transport\_utils.c:1940           | `url_tok[0]` is not freed<br><code>url_tok[1]</code> is not freed<br><code>url_tok</code> is not freed <br>
<tr><td> http_transport_utils.c:2660             </td><td> <code>rest_disp</code> is not freed </td></tr>
<tr><td> http_transport_utils.c:2661             </td><td> <code>handler_desc</code> of <code>handler</code> is not freed <code>**</code> </td></tr>
<tr><td> http_client.c:152<code>*</code>                  </td><td> <code>http_client-&gt;data_stream</code> is not freed <code>**</code> </td></tr>
<tr><td> http_worker.c:118                       </td><td> <code>out_stream</code> may be lost before frist use (:270), also it may be lost in <code>&gt;</code> 10 places </td></tr>
<tr><td> http_worker.c:268                       </td><td> <code>response</code> will be freed by msg_ctx <code>***</code> </td></tr>
<tr><td> http_worker.c:324                       </td><td> <code>response</code> will be freed by msg_ctx <code>***</code> </td></tr>
<tr><td> http_worker.c:325<code>*</code>                  </td><td> <code>msg_ctx</code> is not freed </td></tr>
<tr><td> http_worker.c:342                       </td><td> <code>accept_header_field_list</code> is not freed </td></tr>
<tr><td> http_worker.c:388                       </td><td> <code>accept_charset_header_field_list</code> is not freed </td></tr>
<tr><td> http_worker.c:437                       </td><td> <code>accept_language_header_field_list</code> is not freed </td></tr>
<tr><td> http_worker.c:888                       </td><td> <code>response</code> will be freed by msg_ctx <code>***</code> </td></tr>
<tr><td> http_worker.c:890<code>*</code>                  </td><td> <code>body_string</code> is not freed, it can be allocated in multiple places </td></tr>
<tr><td> http_worker.c:890                       </td><td> <code>out_stream</code> is not freed <code>**</code> </td></tr>
<tr><td> http_worker.c:922                       </td><td> <code>url_ext_form</code> must be freed in another branches too <code>**</code> </td></tr>
<tr><td> http_worker.c:1777                      </td><td> <code>response</code> double freed </td></tr>
<tr><td> http_worker.c:1196<code>*</code>                 </td><td> <code>url_ext_form</code> is not freed, <code>msg_ctx</code> is not freed </td></tr>
<tr><td> http_worker.c:1196<code>*</code>                 </td><td> <code>msg_ctx</code> is not freed </td></tr>
<tr><td> http_worker.c:1196<code>*</code>                 </td><td> <code>out_stream</code> is not freed </td></tr>
<tr><td> http_worker.c:1316                      </td><td> <code>response</code> will be freed by msg_ctx <code>***</code> </td></tr>
<tr><td> http_worker.c:1429<code>*</code>                 </td><td> <code>url_ext_form</code> is not freed, <code>msg_ctx</code> is not freed </td></tr>
<tr><td> http_worker.c:1429<code>*</code>                 </td><td> <code>msg_ctx</code> is not freed </td></tr>
<tr><td> http_worker.c:1429<code>*</code>                 </td><td> <code>out_stream</code> is not freed </td></tr>
<tr><td> http_worker.c:1475                      </td><td> <code>response</code> will be freed by msg_ctx <code>***</code> </td></tr>
<tr><td> http_worker.c:1976<code>*</code>                 </td><td> <code>out_stream</code> is not freed </td></tr>
<tr><td> http_worker.c:2008                      </td><td> <code>response</code> will be freed by msg_ctx <code>***</code> </td></tr>
<tr><td> http_worker.c:2026                      </td><td> <code>response_stream</code> of <code>response</code> is not freed <code>***</code> </td></tr>
<tr><td> http_worker.c:2026                      </td><td> <code>msg_ctx</code> is not freed <code>***</code> </td></tr>
<tr><td> http_worker.c:2030                      </td><td> <code>url_ext_form</code> is not freed </td></tr>
<tr><td> http_simple_response.c:537              </td><td> <code>simple_response-&gt;stream</code> is not freed <code>**</code> <code>***</code> </td></tr>
<tr><td> msg_ctx.c:441                           </td><td> <code>msg_ctx-&gt;out_transport_info</code> may be not freed on client or server <code>**</code> <code>***</code> </td></tr>
<tr><td> msg_ctx.c:557<code>*</code>                      </td><td> <code>msg_ctx-&gt;op_ctx</code> may be not freed in some situations </td></tr>
<tr><td> core_utils.c:1186                       </td><td> multiple(5) possibilities to get memleak <code>axutil_hash_index_t hi</code> by <code>return</code> or <code>break</code> operator </td></tr>
<tr><td> simple_http_svr_conn.c:310              </td><td> <code>str_line</code> is not freed </td></tr>
<tr><td> raw_xml_in_out_msg_recv.c:382           </td><td> <code>axiom_node_to_string</code> result is not freed </td></tr>
<tr><td> options.c:526                           </td><td> previous <code>property</code> value is not freed </td></tr>
<tr><td> mime_parser.c:365                       </td><td> multiple chances(13) to leak <code>temp_mime_boundary</code> </td></tr>
<tr><td> http_transport_utils.c:372<code>*</code>         </td><td> <code>callback_ctx</code> is not freed </td></tr>
<tr><td> http_transport_utils.c:571              </td><td> <code>mime_boundary</code> is not freed </td></tr>
<tr><td> http_worker.c:1189                      </td><td> <code>response</code> stream is not freed in case of error </td></tr></tbody></table>


  * `*` mark - memory was definetely allocated in branch operator (if/then/else), this is a line after which it must be freed.
  * `**` - memory leak caused by leaving object unfreed in hope it will be freed somewhere later, but not freed in some branches.
  * `***` - rewritten logic to avoid memleaks.


## Known memleaks to fix ##

There is draft list how to reproduce memory leak:

echo\_non\_blocking\_dual: soap\_builder.c:120 - soap\_builder is not freed

echo\_blocking\_auth: op\_client.c:1212 - msg\_ctx is not freed

yahoo client: http\_transport\_utils.c:2240 - chunked\_stream is not freed

mtom\_callback: causes multiple memleaks on server side

Failed REST POST, PUT (service not found) methods causes multiple leaks on server side.