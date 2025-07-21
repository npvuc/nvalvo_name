

---

# Example:_Composing_an_HTML_File

The following example calls the composition pipeline for an HTML file composition.

```
/*
* ComposerExample is an example of calling the Composition pipeline
* using the AOM Composer. In this example, an XML document is
* composed into an HTML file. The source document can exist in one
* of 2 places:
* - in Arbortext.
* - in a file.
* The Composition uses the htmlfile pipeline defined in htmlfile.ccf
* in the composer directory.
*/
import com.arbortext.epic.*;
import org.w3c.dom.*;
import java.io.File;
public class ComposerExample {
/**
* Used internally to access the composer configuration file.
*/
private static final String HTMLFILE_CCF =
File.separator + "composer" + File.separator + "htmlfile.ccf";
/**
* Used internally to access the entity substitution file.
*/
private static final String HTMLENTSUBFILE =
File.separator + "composer" + File.separator + "htmlEntSub.xml";
/**
* Produces HTML from an in-memory XML file and an XSL stylesheet.
*
* @param docId Id of document to process.
*
* @param stylesheet Fully-pathed XSL stylesheet.
*
* @param outputFile Fully-pathed HTML output filename.
*/
public static void composeToHtmlFromDoc(int docId, String stylesheet,
String outputFile) {
boolean calledStartJob = false;
try {
String installPath = Acl.eval("main::aptpath");
//Create the Composer object for the HTML composition process.
Composer composer = Application.createComposer(installPath +
HTMLFILE_CCF);
PropertyMap params = Application.createPropertyMap();
//Set up the parameters .
params.putString("stylesheet", stylesheet);
params.putString("document", Integer.toString(docId));
//the entity substitution file for HTML
params.putString("html.entSubFname", installPath + HTMLENTSUBFILE);
params.putString("outputFile", outputFile);
//The following sets up the directory where any graphics would
//be placed and the associated href in the HTML document.
params.putString("graphicsHref", (new File(outputFile)).getName()
+ ".graphics/");
params.putString("graphicsPath", outputFile + ".graphics/");
// Let the composer know we are using an XSL stylesheet as opposed
// to a FOSI ("fosi").
params.putString("stylesheetType", "xsl");
//The Acl.* methods perform some initialization that needs to
//happen for the Composer Log.
Acl.execute("require _composerlog");
Acl.execute("require _eventlog");
//The start_job method MUST be called before the composition process
//is run.
Acl.func("_composerlog::start_job", "ComposerExample");
calledStartJob = true;
//Set the log level to info.
String SEVERITY_INFO = Acl.func("eval", "_eventlog::SEVERITY_INFO");
Acl.func("_composerlog::set_log_severity", SEVERITY_INFO);
//runPipeline returns a boolean indicating success or failure.
if (composer.runPipeline(params)) {
Acl.func("_composerlog::add_record", SEVERITY_INFO, "Success.");
}
else {
// Error information will have been placed into the Composer Log.
Acl.func("_composerlog::add_record", SEVERITY_INFO, "Failure.");
}
}
catch (AclException ex) {
// Unexpected.
System.err.println("ACLException in composeToHtmlFromDoc: " + ex);
ex.printStackTrace(System.err);
}
catch (AOMException aomex) {
// Unexpected.
System.err.println("AOMException in composeToHtmlFromDoc: " + aomex);
aomex.printStackTrace(System.err);
}
finally {
//Cleanup code to tell the ComposerLog that processing is over.
// This MUST be called if start_job was called.
if (calledStartJob) {
Acl.func("_composerlog::end_job");
}
}
}
/**
* Produces HTML from an on-disk XML file and an XSL stylesheet.
*
* @param inputFile Fully-pathed XML filename.
*
* @param stylesheet Fully-pathed XSL stylesheet.
*
* @param outputFile Fully-pathed HTML output filename.
*/
public static void composeToHtmlFromFile(String inputFile,
String stylesheet, String outputFile) {
ADocument doc = null;
try {
doc = (ADocument) Application.openDocument(inputFile);
composeToHtmlFromDoc(doc.getAclId(), stylesheet, outputFile);
}
catch (AOMException aomex) {
System.err.println("AOMException in composeToHtmlFromFile: " + aomex);
aomex.printStackTrace(System.err);
}
finally {
if (doc != null) {
doc.close();
}
}
}
}
```



---

# Related_AOM_Interfaces_and_Methods

You can use the following AOM interfaces and methods to obtain information about a composer: