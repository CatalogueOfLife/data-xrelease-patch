# COL XRelease Patch Data
A small [TextTree](https://github.com/gbif/text-tree) dataset that acts as a "patch" dataset for the Catalogue of Life eXtended Release.
It is hosted in Checklistbank at: https://www.dev.checklistbank.org/dataset/271399

## Files
The main taxonomy tree lives in [taxonomy.txtree](taxonomy.txtree). 
Information about the dataset as a whole and how to cite it is kept in metadata.yaml,
while structured references are managed in [BibTex](reference.bib). 
References from this list can then be [cited in the taxonomy file](https://github.com/CatalogueOfLife/coldp/blob/master/docs/publishing-guide-txtree.md).

### BibTex References
BibTex content can be retrieved from CrossRef for most DOIs when known.
For example by using curl on the terminal like this:
> curl --location --silent --header "Accept: application/x-bibtex" https://doi.org/10.1080/11035890601282097 
> @article{Eriksson_2006,
    doi = {10.1080/11035890601282097},
    url = {https://doi.org/10.1080%2F11035890601282097},
    year = 2006,
    month = {jun},
    publisher = {Informa {UK} Limited},
    volume = {128},
    number = {2},
    pages = {97--101},
    author = {Mats E. Eriksson},
    title = {Polychaete jaw apparatuses and scolecodonts from the Silurian Ireviken Event interval of Gotland, Sweden},
    journal = {{GFF}}
}

There are also online editors, e.g. https://truben.no/latex/bibtex/#


## Contribute using Github webhooks
Once the dataset is created in ChecklistBank (CLB), Github webhooks can be used to automatically update the copy in ChecklistBank 
whenever a commit to the repository happens. Configure:

 a) the dataset access URL in CLB to point to the github repo zip archive, e.g. https://github.com/CatalogueOfLife/data-vespoidea/archive/refs/heads/master.zip
 b) the github repo webhook in settings to point to http://api.checklistbank.org/importer/{DATASET_KEY}/github
 c) configure github to use a secret that the CLB admin hands over to you confidently. Please contact mdoering@gbif.org for this!


## Git precommit hook
If you plan to contribute and commit changes 
please configure a git pre commit hook to automatically update the issued date of your metadata.yaml.
For this create a file called `pre-commit.hook` and place it into your `.git/hooks` folder.

```bash
#!/bin/sh
#
d=`date +%Y-%m-%d`
sed -i '' "s/^issued: 20..-..-..$/issued: $d/g" metadata.yaml
git add metadata.yaml
echo "Updated issued in metadata.yaml"
exit 0
```
