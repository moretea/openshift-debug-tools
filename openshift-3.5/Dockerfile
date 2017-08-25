FROM alpine
RUN apk --no-cache add curl bind-tools

# Install OpenShift client
ENV OC_CLIENT_VERSION v3.6.0-rc.0
ENV OC_CLIENT_GIT_COMMIT_PREFIX 98b3d56
ENV OC_CLIENT_SHA=a836046229f41dd098254ef1f7975d65f68f8ea4a84fbacfb66322bbc7c62fa5
RUN export OC_DOWNLOAD_URL=https://github.com/openshift/origin/releases/download/$OC_CLIENT_VERSION/openshift-origin-client-tools-v3.6.0-rc.0-98b3d56-linux-64bit.tar.gz  && \
    export OC_TMP_DOWNLOAD_PATH=/tmp/openshift-origin-tools.tar.gz && \
    curl --silent -L $OC_DOWNLOAD_URL -o $OC_TMP_DOWNLOAD_PATH  && \
    tar -C /tmp -xzf $OC_TMP_DOWNLOAD_PATH && \
    export OC_EXTRACTED_FILES_PATH=/tmp/openshift-origin-client-tools-$OC_CLIENT_VERSION-$OC_CLIENT_GIT_COMMIT_PREFIX-linux-64bit &&\
    mv $OC_EXTRACTED_FILES_PATH/oc /usr/bin/oc && \
    rm -rf $OC_EXTRACTED_FILES_PATH && \
    ((echo "$OC_CLIENT_SHA  /usr/bin/oc" | sha256sum -c -s) || (echo "SHASUM of oc failed" >&2; exit 1))

# Install kubectl
ENV KUBECTL_VERSION=1.5.2
ENV KUBECTL_SHA=6a694ca36853ef5870dd86dab5db1a06dd69f202f212ba37c736fd009ea1ce91
RUN curl --silent https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl -o /usr/bin/kubectl && \
    chmod +x /usr/bin/kubectl && \
    sha256sum /usr/bin/kubectl && \
    ((echo "$KUBECTL_SHA  /usr/bin/kubectl" | sha256sum -c -s) || (echo "SHASUM of kubectl failed" >&2; exit 1))
