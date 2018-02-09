# Moodle Data Cleaning Parameters
The following is an overview of the parameter cleaning types to be used with 
## required_param(), optional_param(), and clean_param().

PARAM_RAW: specifies a parameter that is not cleaned or processed in any way.
PARAM_CLEAN: Obsolete, please try to use a more specific type of parameter.
PARAM_INT: Integers only, use when expecting only numbers
PARAM_INTEGER: Alias for PARAM_INT
PARAM_ALPHA: Contains only english letters.
PARAM_ACTION: Alias for PARAM_ALPHA, use for various actions in forms and URLs.
PARAM_FORMAT: Alias for PARAM_ALPHA, use for names of plugins, formats, etc.
PARAM_NOTAGS: All HTML tags are stripped from the text. Do not abuse this type.
PARAM_MULTILANG: Alias of PARAM_TEXT.
PARAM_TEXT: General plain text compatible with multilang filter, no other html tags.
PARAM_FILE: Safe file name, all dangerous chars are stripped, protects against XSS, SQL injections and directory traversals.
PARAM_PATH: Safe relative path name, all dangerous chars are stripped, protects against XSS, SQL injections and directory traversals
note: The leading slash is not removed, window drive letter is not allowed
PARAM_HOST: expected fully qualified domain name (FQDN) or an IPv4 dotted quad (IP address)
PARAM_URL: expected properly formatted URL.
PARAM_LOCALURL: expected properly formatted URL as well as one that refers to the local server itself. NOT orthogonal to the others! Implies PARAM_URL!
PARAM_CLEANFILE: safe file name, all dangerous and regional chars are removed,
PARAM_ALPHANUM: expected numbers and letters only.
PARAM_BOOL: converts input into 0 or 1, use for switches in forms and urls.
PARAM_CLEANHTML: cleans submitted HTML code and removes slashes
note: do not forget to addslashes() before storing into database!
PARAM_ALPHAEXT: the same contents as PARAM_ALPHA plus the chars in quotes: "/-_" allowed, suitable for include() and require()
PARAM_SAFEDIR: safe directory name, suitable for include() and require()
PARAM_SEQUENCE: expects a sequence of numbers like 8 to 1, 5, 6, 4, 6, 8, 9. Numbers and commas only.
