/*
MARKDOWN, Introduce the tutorial

*/
RequireVersion ("2.4.0");

// ##############################
//   Imports
// ##############################
LoadFunctionLibrary ("libv3/tasks/alignments.bf");
LoadFunctionLibrary("libv3/IOFunctions.bf");
LoadFunctionLibrary("libv3/UtilityFunctions.bf");

// ##############################
//  Declares
// ##############################

A = {"Carbon": 5, "Nitrogen": 5, "Oxygen": 0, "Hydrogen": 5};
T = {"Carbon": 5, "Nitrogen": 2, "Oxygen": 2, "Hydrogen": 6};
C = {"Carbon": 4, "Nitrogen": 2, "Oxygen": 1, "Hydrogen": 6};
G = {"Carbon": 4, "Nitrogen": 6, "Oxygen": 1, "Hydrogen": 5};

nucleotides = {}; // empty dictionary

// ##############################
//  Read in file
// ##############################
fprintf (stdout, "# Reading fasta file 'ncov.fas' from current directory \n");
DataSet alignment = ReadDataFile ('ncov.fas');
fprintf (stdout, alignment, "\n");

// ##############################
//  Set up output table
// ##############################

output.table_output_options = {
    utility.getGlobalValue("terms.table_options.header"): TRUE,
    utility.getGlobalValue("terms.table_options.minimum_column_width"): 10,
    utility.getGlobalValue("terms.table_options.align"): "center",
    utility.getGlobalValue("terms.table_options.column_widths"): {
        "0": 22,
        "1": 22,
        "2": 22,
        "3": 22,
        "4": 22,
        "5": 22,
        "6": 22
    }
};

output.report = {
    {
        "Sequence ID", "Sequence Length", "Total Carbon Atoms", "Total Hydrogen Atoms", "Total Oxygen Atoms", "Total Nitrogen Atoms", "Molecular Weight"
    }
};

fprintf (stdout, "\n### SUMMARY ###\n");

fprintf(stdout, "\n",  io.FormatTableRow(output.report, output.table_output_options));

// ##############################
//  Main loop
// ##############################
for (sequence_index = 0; sequence_index < alignment.species; sequence_index+=1) {
  GetDataInfo (ith_sequence, alignment, sequence_index);
  GetString (seq_name, alignment, sequence_index);
  
  nucleotides_per_seq = {};
  nucleotides [ith_sequence[0]] += 1;
  nucleotides_per_seq [ith_sequence[0]] += 1;
  
  for (character_index = 1; character_index < Abs (ith_sequence); character_index += 1) {
    nucleotides [ith_sequence[character_index]] += 1;
    nucleotides_per_seq [ith_sequence[character_index]] += 1;
    //dinucleotides [ith_sequence[character_index-1][character_index]] += 1;
  } // end inner for
  
  //fprintf (stdout, "\n ", seq_name, nucleotides_per_seq, "\n");
  seq_length = nucleotides_per_seq['A'] + nucleotides_per_seq['C'] + nucleotides_per_seq['G'] + nucleotides_per_seq['T'];
  //fprintf (stdout, "\n ", seq_name, " total NTs: ", total);
  
  fprintf(stdout, io.FormatTableRow(
      {
       {
       seq_name,
       seq_length,
       (nucleotides_per_seq['T'] * T["Carbon"]) + (nucleotides['C'] * C["Carbon"]) + (nucleotides['G'] * G["Carbon"]) + (nucleotides['A'] * A["Carbon"]),
       (nucleotides_per_seq['T'] * T["Hydrogen"]) + (nucleotides['C'] * C["Hydrogen"]) + (nucleotides['G'] * G["Hydrogen"]) + (nucleotides['A'] * A["Hydrogen"]),
       (nucleotides_per_seq['T'] * T["Oxygen"]) + (nucleotides['C'] * C["Oxygen"]) + (nucleotides['G'] * G["Oxygen"]) + (nucleotides['A'] * A["Oxygen"]),
       (nucleotides_per_seq['T'] * T["Nitrogen"]) + (nucleotides['C'] * C["Nitrogen"]) + (nucleotides['G'] * G["Nitrogen"]) + (nucleotides['A'] * A["Nitrogen"]),
       "N/A"
       }
      },
      output.table_output_options)
  );
  
  
} // End outer for

fprintf (stdout, "\n");


//fprintf (stdout, "\nNucleotide counts: ", nucleotides, "\n\nDinucleotide counts: ", dinucleotides, "\n");
//fprintf (stdout, "\n### SUMMARY ###\n");

//fprintf (stdout, "\n# TOTAL Nucleotide counts: ", nucleotides, "\n");
//total = nucleotides['A'] + nucleotides['C'] + nucleotides['G'] + nucleotides['T'];


// Print pretty table here
// Sequence ID, Sequence Length, Carbon, Hydrogen, Oxygen, Nitrogen, Molecular weight

// fprintf(stdout, io.FormatTableRow(output.report, output.table_output_options));

// ##############################
//   End of file
// ##############################


/*
for (seq_id = 0; seq_id < alignment.species; seq_id += 1) {
  GetString (seq_name, alignment, seq_id);
  GetDataInfo (seq_data, alignment, seq_id);
  fprintf (stdout, "ID = ", seq_name, "\n");
  // fprintf (stdout, "sequence = ", seq_data, "\n");
}
*/
