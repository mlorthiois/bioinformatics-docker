FROM continuumio/miniconda3:latest

COPY environment.yml /opt/environment.yml

RUN conda env update -n base -f /opt/environment.yml && \
    conda clean -afy && \
    rm /opt/environment.yml && \
    apt update && \
    apt install \
        -y \
        --no-install-recommends \
        --no-install-suggests \
        build-essential && \
    apt-get clean && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* && \
    git clone https://github.com/ConesaLab/SQANTI3.git /opt/sqanti3 && \
    rm -rf /opt/sqanti3/.git && \
    rm -rf /opt/sqanti3/example && \
    wget -q http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/gtfToGenePred -P /opt/sqanti3/utilities/ && \
    chmod +x /opt/sqanti3/utilities/gtfToGenePred && \
    git clone https://github.com/Magdoll/cDNA_Cupcake.git /opt/cDNA_Cupcake && \
    cd /opt/cDNA_Cupcake && \
    python setup.py build && \
    python setup.py install && \
    rm -rf /opt/cDNA_Cupcake/.git && \
    rm -rf /opt/cDNA_Cupcake/.git

ENV PYTHONPATH /opt/cDNA_Cupcake/sequence/
ENV PATH "$PATH:/opt/sqanti3/"

CMD [ "sqanti3_qc.py" ]