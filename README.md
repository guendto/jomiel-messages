# jomiel-messages

The Python bindings for the [jomiel] protobuf messages.

## About

The purpose of this project is to provide the [jomiel] protobuf message
bindings package that are `easy to install` from PyPI. The bundled have
been generated from the protobuf declaration files of [jomiel-proto].

## License

`jomiel-messages` is licensed under the [Apache License version
2.0][aplv2].

## Installation

```shell
pip install jomiel-messages
```

## Usage

Serialize an inquiry message:

```python
from jomiel_messages.protobuf.v1alpha1.message_pb2 import Inquiry

inquiry = Inquiry()
inquiry.media.input_uri = 'https://foo.bar/baz'
serialized_string = Inquiry.SerializeToString(inquiry)
# ...
```

De-serialize a response message:

```python
from jomiel_messages.protobuf.v1alpha1.message_pb2 import Response
from jomiel_messages.protobuf.v1alpha1.status_pb2 import STATUS_CODE_OK

response = Response()
response.ParseFromString(serialized_string)

if response.status.code != STATUS_CODE_OK:
  print(f"message={response.status.message})
  print(f"status-code={response.status.code}")
  print(f"error-code={response.status.error}")
  print(f"http-code={response.status.http.code}")
  # ...
else:
  # ...
```

## Building packages from repo

```shell
./bin/gen
pip install pep517
python -m pep517.build .
```

See dist/ for the packages.

## Acknowledgements

### Subprojects

`jomiel-messages` has the following subtrees (see git-subtree):

- [src/jomiel_messages/proto/](src/jomiel_messages/proto/) of [jomiel-proto]

[jomiel-proto]: https://github.com/guendto/jomiel-proto/
[jomiel]: https://github.com/guendto/jomiel
[aplv2]: https://www.tldrlegal.com/l/apache2