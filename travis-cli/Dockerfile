FROM ruby:2.7.2@sha256:a6a38da33f10468223963ba1f173318b19460afc494f28f2be171bc79e9ce66b
RUN gem install travis -v 1.8.9
RUN travis --version
CMD ["travis","whoami"]
