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


# Moodle Functions for Roles and Capabilities  require_login() get_context_instance() require_capability()  has_capability()
There are several important functions in Moodle in the roles and capabilities system.

The first line of defense in a script is the require_login() function to restrict access to logged-in users. This function first checks that the user is logged in and then optionally checks whether they are allowed to be in a particular course and/or view a particular course module.

To check a user's permission for a capability in a certain context requires a couple of functions. The first, get_context_instance(), returns a context instance as an object. A context instance is a context level (e.g. CONTEXT_COURSE) and an instance id (e.g., a course id).

Once you have the context instance you can require a capability in a script using the function require_capability() or you can check to see if a user has a particular capability before performing some action with the function has_capability(). An application of these functions might look like this:

$context = get_context_instance(CONTEXT_COURSE, $courseid);
$require_capability('moodle/course:view', $context);
// some things that anyone with moodle/course:view can 
// do or see here
// now check for a more restrictive capability
    if (has_capability('moodle/course:update' $context) {
    // do some update to the course
    } else {
        error('You do not have the correct permissions');
}

