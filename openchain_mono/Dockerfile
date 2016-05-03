FROM microsoft/aspnet:1.0.0-rc1-update1

# force update to 1.0.0-rc1-update2
ENV DNX_VERSION 1.0.0-rc1-update2

RUN curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.sh | DNX_USER_HOME=$DNX_USER_HOME DNX_BRANCH=v$DNX_VERSION sh
RUN bash -c "source $DNX_USER_HOME/dnvm/dnvm.sh \
	&& dnvm install $DNX_VERSION -alias default \
	&& dnvm alias default | xargs -i ln -s $DNX_USER_HOME/runtimes/{} $DNX_USER_HOME/runtimes/default"


RUN mkdir /openchain
COPY project.json /openchain/project.json

WORKDIR /openchain

RUN cd /openchain \
    && dnu restore

EXPOSE 9090
ENTRYPOINT ["dnx", "start", "--server.urls", "http://0.0.0.0:9090"]
