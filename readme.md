# Deploy FastAPI on IIS:

## 1. add new site in IIS.

## 2. run this command "pip install wfastcgi".

## 3. run wfastcgi-enable as an administrator to enable wfastcgi in the IIS configuration.

        ### - C:\PROJECT-PATH\venv\Scripts\wfastcgi-enable.exe (run as administrator)

## 4. put the following code in web.config (c:\inetpub\wwwroot\PROJECT-FOLDER\web.config):

    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
        <system.webServer>
            <handlers accessPolicy="Read, Execute, Script">
                <add name="PythonHandler"
                    path="*"
                    verb="*"
                    modules="FastCgiModule"
                    scriptProcessor="C:\PROJECT-PATH\venv\Scripts\python.exe|C:\PROJECT-PATH\venv\lib\site-packages\wfastcgi.py"
                    resourceType="Unspecified"
                    requireAccess="Script" />
            </handlers>
            <directoryBrowse enabled="true" />
        </system.webServer>
        <appSettings>
            <add key="PYTHONPATH"
                value="PROJECT-PATH" />
            <add key="WSGI_HANDLER"
                value="<Base App File Name >.< Your Name App instance >" />
        </appSettings>
    </configuration>
    ```

## 5. Add the following code to 'Base App File Name':

    ```
    from a2wsgi import ASGIMiddleware
    wsgi_app = ASGIMiddleware(app)
    ```
