# DigitalTA

## Usage

Install the following:

```shell
% pip3 install llama_index
% pip3 install torch transformers sentencepiece Pillow
% pip3 install pypdf
% !pip3 install pytube
% pip3 install pydub
% brew install ffmpeg // assuming you are on Mac silicon, which everyone is...
```

Provide an OpenAI access token:

```shell
% export OPENAI_API_KEY=sk-.....
```

Populate the `/data` folder with your tuning data. For example, to download the audio for all BioE lectures from `https://introbioe.stanford.edu/lectures-interviews`, run

```shell
% python3 download_audio.py 
```

Some of these files will be too big for `OpenAI Whisper` to transcribe, so:

```shell
% python3 segment_audio.py 
```

Then, transcribe the audio:

```shell
% python3 transcribe.py 
```

Finally, run the indexer, if you have added new tuning data or if this is the first time you are running the system:

```shell
% cd bioe80
% python3 create_index.py

Generating new index
Loaded 964 docs. Please be patient...
```

Now, try it out....

```shell
% python3 query.py
```

## Methods

Downloaded all of https://github.com/Stanford-BioE80/Stanford-BioE80.github.io

Downloaded all of https://introbioe.stanford.edu

Indexed all `.md`, `.txt`, and `.pdf` files

## Unedited Question/Answer Pairs

These were not human-editied - this is raw output from the model.

*What is the goal of BioE80?*

The goal of BioE80 is to help students learn ways of thinking about engineering living matter, empower them to explore and do bioengineering starting from DNA, become more capable of learning and explaining bioengineering to themselves and others, and devise and express their wishes for bioengineering as might be made true by or before 2030, with the ultimate aim of benefiting all people and the planet.

*Help me to understand abstraction*

Abstraction is a way of simplifying complex systems by breaking them down into smaller, more manageable parts. It is a way of organizing information and ideas into categories and levels, allowing us to focus on the most important aspects of a system. Abstraction can be used to identify patterns and relationships between different parts of a system, and to make it easier to understand how the system works. Abstraction can also be used to create models of systems, which can be used to make predictions about how the system will behave in different situations.

*What is living matter?*

Living matter is any material composed of cells that are capable of growth, metabolism, response to stimuli, and reproduction. Living matter is distinguished from inert matter by its ability to self-organize, adapt, and evolve. Living matter is composed of complex molecules and structures that are organized on many orders of magnitude, from nanometers to meters. Living matter is capable of performing complex functions, such as sensing, responding, and self-repairing.

*Can living matter self-organize?*

Yes, living matter can self-organize. This is evidenced by the fact that living matter is intricately organized on multiple time and spatial scales, and is capable of self-mixing, self-healing, and self-replicating.

*How can I synthesize DNA? [BAD ANSWER before Tuning]*

To synthesize DNA, you can use a four-key keyboard to input raw chemicals that are not derived from existing DNA. You can then play with the chemicals to get the desired DNA sequence. Additionally, you can optimize synthetic chemistry for accuracy to ensure that the DNA sequence is correct.

*How can I synthesize DNA? [after Tuning]*

DNA can be synthesized by first designing the sequence, then synthesizing oligonucleotides (oligos) from the sequence, and finally assembling the oligos into double-stranded DNA (dsDNA) fragments. This process is known as artificial DNA synthesis and is a fundamental tool of synthetic biology. The oligos are synthesized using a process called phosphoramidite-based oligo synthesis, which involves building the oligo chain on a solid support through cycles of chemical reactions. The dsDNA fragments are then assembled using polymerase cycling assembly.

*Bioengineers will...*

One example of an impact of bioengineering today is the development of gene therapy. Gene therapy is a technique used to treat genetic diseases by introducing a gene into a person's cells to replace a mutated gene. This technique has been used to treat diseases such as cystic fibrosis, muscular dystrophy, and hemophilia. It has also been used to treat cancer, HIV, and other diseases. References: https://www.genome.gov/genetics-glossary/Gene-Therapy, https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6111790/, https://www.hopkinsmedicine.org/health/treatment-tests-and-therapies/gene-therapy.

In the future, I wish to realize a world where bioengineering is used to improve the quality of life for all people. Bioengineering should be used to develop treatments and cures for diseases, create sustainable food sources, and develop renewable energy sources. Success would be defined as a world where everyone has access to the treatments and cures they need, where food is plentiful and sustainable, and where renewable energy sources are widely available. To realize this future, we need to focus on developing new technologies, such as gene editing, that can be used to create treatments and cures for diseases. We also need to focus on developing sustainable food sources and renewable energy sources. Finally, we need to create policies that ensure that everyone has access to the treatments and cures they need.

## Conversation example - unedited/raw output

*What's the best way to synthesize DNA?*

The best way to synthesize DNA is to use a combination of oligonucleotide synthesis and assembly techniques. Oligonucleotides can be synthesized using phosphoramidate chemistry, and then assembled into larger DNA fragments using overlap extension PCR. This method allows for the synthesis of DNA fragments up to 100 or 50 bases in length with high fidelity. However, it is not suitable for synthesizing repeated sequences. To overcome this limitation, it is possible to use templated DNA synthesis with a polymerase to fill in the gaps between the short synthesized regions. Additionally, the cost of DNA synthesis and sequencing is decreasing rapidly due to Moore's law, making it more accessible to researchers.

*Can you explain more about oligo assembly*

Oligo assembly is a process of joining short synthetic DNA fragments together to form longer DNA strands. This is done by using enzymes to join the fragments together in a specific order. The process is often used to create custom DNA strands for research or other applications. The process can be done manually or with automated systems. Automated systems are often used to increase the speed and accuracy of the assembly process.

## Main impressions

Training on the 781 RAW documents took 3 mins on my laptop. Some answers are great and some are _initially_ crazy/dumb (see e.g. "How can I synthesize DNA?[BAD ANSWER before Tuning]") and can be improved withing a few seconds by adding material relevant to the question (see e.g. "How can I synthesize DNA?[after Tuning]"). Tuning with relevant material immediately helps. The system does best when there is training material that is similar to the question/prompt. The system does best when trained with essays and question/answer pairs.
