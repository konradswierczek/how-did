# RStudio Server in WSL

Working on Windows is a common affliction experienced by researchers everywhere: both by choice and necessity. WSL can make it a lot easier to cope! While I generally prefer to have my projects in containers or virtual environments, it can be nice to have a simple working environment for general tasks. It's especially nice if you depend heavily on R Tidyverse and Quarto for document preparation and analysis. Here's how I configure my "playground" WSL environment before I start making a mess of it with all sorts of other tools. Rather than using remotes or terminal text editors, I can pop into the browser and use RStudio anytime, which makes it great for demos.

This assumes you're already up and running with WSL and can get Ubuntu loaded in.
Start inside of your WSL Ubuntu distro.

```bash
# Update package lists and install necessary system dependencies.
sudo apt update -y
sudo apt install -y gdebi-core libssl-dev libcurl4-openssl-dev libxml2-dev libfreetype6-dev \
    libharfbuzz-dev libfontconfig1-dev libfribidi-dev libpng-dev libtiff5-dev libjpeg-dev

# Install the R programming language.
sudo apt install -y r-base

# Download and install RStudio Server.
RSTUDIO_VERSION="2024.12.0-467"
wget -q "https://download2.rstudio.org/server/jammy/amd64/rstudio-server-${RSTUDIO_VERSION}-amd64.deb"
sudo gdebi -n "rstudio-server-${RSTUDIO_VERSION}-amd64.deb"
# Clean up after yourself.
rm "rstudio-server-${RSTUDIO_VERSION}-amd64.deb"

# Get Python ready to go while we're at it.
sudo apt install python3-venv python3-pip python3-dev
```

You should now be able to access RStudio Server from `localhost:8787`.

Next, install Quarto for document preparartion with both R and Python. The first time you run a python file, RStudio will help you get setup with Python support in Quarto.

```bash
# Download and install Quarto CLI.
QUARTO_VERSION="1.6.40"
wget -q "https://github.com/quarto-dev/quarto-cli/releases/download/v${QUARTO_VERSION}/quarto-${QUARTO_VERSION}-linux-amd64.tar.gz"
mkdir -p ~/opt
tar -xzf "quarto-${QUARTO_VERSION}-linux-amd64.tar.gz" -C ~/opt
# Clean up after yourself.
rm "quarto-${QUARTO_VERSION}-linux-amd64.tar.gz"

# Add Quarto CLI to the PATH.
echo 'export PATH="$HOME/opt/quarto-${QUARTO_VERSION}/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

Finally, add some packages to make R and Quarto more functional.

```r
# Install the tidyverse (who want's to use vanilla r?).
install.packages("tidyverse")

# Add latex if exporting to PDF.
install.packages("tinytex")
tinytex::install_tinytex()
```
