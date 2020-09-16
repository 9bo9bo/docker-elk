ARG ELK_VERSION

# https://www.docker.elastic.co/
FROM docker.elastic.co/elasticsearch/elasticsearch:${ELK_VERSION}

ARG ELK_VERSION
ARG SUDACHI_PLUGIN_VER

# Add your elasticsearch plugins setup here
# Example: RUN elasticsearch-plugin install analysis-icu

RUN elasticsearch-plugin install \
  analysis-kuromoji \
  analysis-icu

# install Sudachi
# see https://tsgkdt.hatenablog.jp/entry/2019/04/09/180738
RUN curl -OL https://object-storage.tyo2.conoha.io/v1/nc_2520839e1f9641b08211a5c85243124a/sudachi/sudachi-dictionary-latest-core.zip && \
    curl -OL https://object-storage.tyo2.conoha.io/v1/nc_2520839e1f9641b08211a5c85243124a/sudachi/sudachi-dictionary-latest-full.zip && \
    unzip -o -d config/sudachi -j  'sudachi-dictionary*.zip'  && \
    rm -f sudachi-dictionary*.zip && \
    bin/elasticsearch-plugin install "https://github.com/WorksApplications/elasticsearch-sudachi/releases/download/v${ELK_VERSION}-${SUDACHI_PLUGIN_VER}/analysis-sudachi-${ELK_VERSION}-${SUDACHI_PLUGIN_VER}.zip"
