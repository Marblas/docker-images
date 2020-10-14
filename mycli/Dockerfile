FROM python:3.9-slim@sha256:fceaa6d4a20e1bec3b049e6b6bfad4859446941257198eb72d9aabb9ee8a1fd4
RUN pip install mycli
ADD ./entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
