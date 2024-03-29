<template>
    <v-container>
        <h1 class="font-weight-light">
            peptfilter
        </h1>
        <h3 class="font-weight-light">Filters peptides based on length and amino acid occurrence.</h3>
        
        <v-divider class="my-2" />

        <p>
            The <Code>peptfilter</Code> command takes one or more (tryptic) peptides as input and returns them as output if they satisfy all filter criteria. 
            By default, peptides with length between 5 and 50 are retained. This command runs entirely locally and doesn't connect to any server. 
        </p>

        <HeaderBodyCard id="input" title="Input">
            <p>
                The <Code>peptfilter</Code> command accepts (tryptic) peptides as input from <i>standard input</i>. A single peptide per line is expected. 
            </p>

            <h4>Example</h4>
            <Boxed>
                <Sentinel>$</Sentinel> cat input.txt
                <br>AAR
                <br>AALTER
                <br><Sentinel>$</Sentinel> cat input.txt | peptfilter
                <br>AALTER
            </Boxed>
        </HeaderBodyCard>

        <HeaderBodyCard id="output" title="Output" class="mt-5">
            <p>
                The <Code>peptfilter</Code> command outputs all input peptides that satisfy all filter criteria to <i>standard output</i>. By default, peptides 
                with a length lower than 5 or higher than 50 are removed. The length filter can be changed by using the <RLink to="#options" router>--minlen</RLink> 
                and <RLink to="#options" router>--maxlen</RLink> parameters. Peptides can also be filtered based on whether or not they lack or contain certain amino 
                acids. This can be done with the <RLink to="#options" router>--lacks</RLink> and <RLink to="#options" router>--contains</RLink> parameters. 
            </p>
        </HeaderBodyCard>

        <HeaderBodyCard id="fasta" title="Fasta support" class="mt-5">
            <p>
                The <Code>peptfilter</Code> command supports input in a fasta-like format (for example generated by the <RLink to="/clidocs/prot2pept" router>prot2pept command</RLink>). 
                This format consists of a fasta header (a line starting with a >), followed by one or more lines containing one peptide each. When this format is detected, 
                the fasta headers will automatically be included in the output. 
            </p>

            <h4>Example</h4>
            <Boxed>
                <Sentinel>$</Sentinel> cat input.txt
                <br>> header 1
                <br>AALTER
                <br>AAR
                <br>LGAALGAGLAVIGAGIGIGK
                <br>> header 2
                <br>PEPTIDE
                <br><Sentinel>$</Sentinel> cat intput.txt | peptfilter
                <br>> header 1
                <br>AALTER
                <br>LGAALGAGLAVIGAGIGIGK
                <br>> header 2
                <br>PEPTIDE
            </Boxed>
        </HeaderBodyCard>

        <HeaderBodyCard id="options" title="Command-line options" class="mt-5">
            <h2>--minlen <span class="text-caption grey--text text--darken-2">Specify minimum length</span></h2>

            <p>
                By default, only peptides with a minimal length of 5 are retained. By using the <Code>--minlen</Code> parameter, this value can be changed. 
            </p>

            <h4>Example</h4>
            <Boxed>
                <Sentinel>$</Sentinel> cat input.txt
                <br>AALTER
                <br>AAR
                <br><Sentinel>$</Sentinel> cat input.txt | peptfilter <b>--minlen</b> 3
                <br>AALTER
                <br>AAR
            </Boxed>

            <h2>--maxlen <span class="text-caption grey--text text--darken-2">Specify maximum length</span></h2>

            <p>
                By default, only peptides with a maximal length of 50 are retained. By using the <Code>--maxlen</Code> parameter, this value can be changed. 
            </p>

            <h4>Example</h4>
            <Boxed>
                <Sentinel>$</Sentinel> cat input.txt
                <br>AALTER
                <br>AAR
                <br><Sentinel>$</Sentinel> cat input.txt | peptfilter <b>--maxlen</b> 4
                <br>AAR
            </Boxed>

            <h2>--contains / -c <span class="text-caption grey--text text--darken-2">Specify mandatory amino acids</span></h2>

            <p>
                By using the <Code>--contains</Code> parameter, you can specify the amino acids that a peptide must contain. All specified amino acids must be 
                present in the peptide for it to be retained. 
            </p>

            <h4>Example</h4>
            <Boxed>
                <Sentinel>$</Sentinel> cat input.txt
                <br>AALTER
                <br>AARAAR
                <br><Sentinel>$</Sentinel> cat input.txt | peptfilter <b>--contains</b> RL
                <br>AALTER
            </Boxed>

            <h2>--lacks / -l <span class="text-caption grey--text text--darken-2">Specify forbidden amino acids</span></h2>

            <p>
                By using the <Code>--lacks</Code> parameter, you can specify the amino acids that a peptide can not contain. The peptide may have none of the 
                specified amino acids for it to be retained. 
            </p>

            <h4>Example</h4>
            <Boxed>
                <Sentinel>$</Sentinel> cat input.txt
                <br>AALTER
                <br>AARAAR
                <br><Sentinel>$</Sentinel> cat input.txt | peptfilter <b>--lacks</b> VL
                <br>AARAAR
            </Boxed>

            <h2>--help / -h <span class="text-caption grey--text text--darken-2">Display help</span></h2>

            <p>
                This flag displays the help. 
            </p>
        </HeaderBodyCard>
    </v-container>
</template>

<script setup lang="ts">
import Code from '@/components/highlights/InlineCode.vue';
import HeaderBodyCard from '@/components/cards/HeaderBodyCard.vue';
import Boxed from '@/components/highlights/Boxed.vue';
import Sentinel from '@/components/highlights/Sentinel.vue';
import RLink from '@/components/highlights/ResourceLink.vue';
</script>
