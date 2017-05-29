# Zip Support

This is a [Codename One](https://www.codenameone.com) library for Zip support based on the code from the [zipme](https://sourceforge.net/projects/zipme/) project. As such it carries a modified GPL license similar to the classpath exception but not similar enough to include in the core distribution.

This library can be used to enable ZIP functionality in Codename One applications.

You can download an install this library from [here](https://github.com/codenameone/ZipSupport/blob/master/ZipSupport.cn1lib?raw=true).


public Unzip(String zipName, String dirDest) 
{

  InputStream is;
  try {
            is = Storage.getInstance().createInputStream(zipName);
            ZipInputStream zipStream = new ZipInputStream(is);
            ZipEntry entry;

            // create a buffer to improve copy performance later.
            byte[] buffer = new byte[2048];

            while ((entry = zipStream.getNextEntry()) != null) {
                String s = entry.getName();
                String outdir = FileSystemStorage.getInstance().getAppHomePath();
                if (outdir.length() > 0)
                {
                    outdir = outdir + "/" + dirDest;
                }
                String outpath = outdir + "/" + entry.getName();
                OutputStream output = null;
                try {
                    output = FileSystemStorage.getInstance().openOutputStream(outpath);
                    int len = 0;
                    while ((len = zipStream.read(buffer)) > 0) {
                        output.write(buffer, 0, len);
                    }
                } finally {
                    // we must always close the output file
                    if (output != null) {
                        output.close();
                    }
                }
            }
        } catch (IOException ex) {
            Log.p(ex.getMessage(), 0);
        }
    }



public Unzip(InputStream zipFile, String dirDest) {

  InputStream is;
        try {
            is = zipFile;
            ZipInputStream zipStream = new ZipInputStream(is);
            ZipEntry entry;

            // create a buffer to improve copy performance later.
            byte[] buffer = new byte[2048];

            while ((entry = zipStream.getNextEntry()) != null) {
                String s = entry.getName();
                String outdir = FileSystemStorage.getInstance().getAppHomePath();
                if (outdir.length() > 0)
                {
                    outdir = outdir + "/" + dirDest;
                }
                String outpath = outdir + "/" + entry.getName();
                OutputStream output = null;
                try {
                    output = FileSystemStorage.getInstance().openOutputStream(outpath);
                    int len = 0;
                    while ((len = zipStream.read(buffer)) > 0) {
                        output.write(buffer, 0, len);
                    }
                } finally {
                    // we must always close the output file
                    if (output != null) {
                        output.close();
                    }
                }
            }
        } catch (IOException ex) {
            Log.p(ex.getMessage(), 0);

        }
    }

}
