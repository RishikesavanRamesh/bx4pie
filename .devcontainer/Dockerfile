FROM ubuntu:latest

# Set noninteractive mode for apt
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    pandoc \
    pandoc-citeproc \
    curl \
    gdebi-core \
    r-base \
    chromium-browser \
    fonts-noto \
    git \
    wget \
    && rm -rf /var/lib/apt/lists/*

# Install TinyTeX
RUN wget -qO- "https://yihui.org/tinytex/install-bin-unix.sh" | sh -s - --admin --no-path

# Add TinyTeX to the PATH
ENV PATH="/root/.TinyTeX/bin/x86_64-linux:$PATH"

# Install some additional LaTeX packages
RUN tlmgr install collection-langenglish

# Install R packages
RUN R -e "install.packages(c('shiny', 'jsonlite', 'ggplot2', 'htmltools', 'remotes', 'renv', 'knitr', 'rmarkdown'), repos='http://cran.rstudio.com/')"

RUN curl -LO https://quarto.org/download/latest/quarto-linux-amd64.deb
RUN gdebi --non-interactive quarto-linux-amd64.deb

# Set it back to interactive mode if needed for subsequent commands
ENV DEBIAN_FRONTEND=dialog

CMD ["bash"]
