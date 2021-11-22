FROM python:3.9.7

WORKDIR /workspace

ENV DEBCONF_NOWARNINGS=yes

RUN apt-get update
RUN apt-get -y install locales && \
    localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
RUN apt-get install -y vim bash-completion

COPY pyproject.toml .

RUN pip install -U pip
RUN pip install poetry \
    && poetry config virtualenvs.create false \
    && poetry install \
    && rm pyproject.toml

# Setting jupyter_notebook_config
RUN jupyter notebook --generate-config
RUN echo "c.NotebookApp.ip = '0.0.0.0'" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.notebook_dir = '/workspace'" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.open_browser = False" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.token = ''" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.password = ''" >> /root/.jupyter/jupyter_notebook_config.py

RUN echo "source /etc/bash_completion" >> ~/.bashrc

EXPOSE 10000
