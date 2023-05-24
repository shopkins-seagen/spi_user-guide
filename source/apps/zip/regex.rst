.. include:: nav.rst

Regular Expression Filters
============================================
The application uses regular expressions(regex) to filter files for both inclusion into Zip archive creation, and extraction of files from an existing Zip archive. These are the 
same as wildcards commonly used from the command line. Providing an invalid regex results in an ERROR. For example, "*" does mean everything in regex as it does in wildcard syntax.

The API using .NET regular expression engine to match by files by name, with matching files selected for inclusion in or extraction from a Zip archive. The compiled regex has the ignore case property set 
by default, so case does not matter. The following table lists some regex patterns that can be passed to the FILTER parameter to control the content. There are limitless possibilities 
for pattern matching which provides flexibility for complete control of the desired content. 

For more details or practice, see `Regex 101 <https://regex101.com/>`__ .


.. list-table::
    :widths: 20 50 30
    :header-rows: 1

    * - Regex
      - Description
      - Matches
    * - .*
      - '.' is a metacharacter that means any, and '*' is a quantifier that mean any amount of. 
      - everything
    * - \\.sas$
      - The '\\' is an escape character that treats the '.' as a literal period. The '$' means ends with. In this example the file must end with '.sas'
      - SAS program files
    * - \.(pdf|xlsx|docx)
      - The values delimited by | inside the parens act like an 'or'
      - Matches .pdf, .xlsx, and .docx files
    * - \.sas(7b)?(dat|cat|itm|$)
      - This is similar to the previous example, except the (7b)? means optional, and the paren match dat, cat, itm, or the string ends '$'
      - .sas, .sas7bdat, .sas7bcat, .sas7bitm
    * - (\.|\/)(?!log|lst|rtf).*$
      - The '?!' is a negative lookahead assertion, which excludes files from matching. the 3 file types in the parens are still and 'or', but this time they are negated. 
      - Matches everything except .log, .lst, and .rtf files. 
    * - ^(t|l|f)-.*\.sas$
      - The ^ means 'starts with'. In this case, the file starts with a t, l, or f, followed by a hypen, then anything for any number of charcters, and ends with .sas
      - Table, listing, and figure SAS programs      






