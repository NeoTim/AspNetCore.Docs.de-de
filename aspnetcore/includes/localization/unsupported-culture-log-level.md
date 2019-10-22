> [!NOTE]
> <span data-ttu-id="985b2-101">Web-Apps vor ASP.NET Core 3.0 schreiben ein Protokoll vom Typ `LogLevel.Warning` pro Anforderung, wenn die angeforderte Kultur nicht unterstützt wird.</span><span class="sxs-lookup"><span data-stu-id="985b2-101">Prior to ASP.NET Core 3.0 web apps write one log of type `LogLevel.Warning` per request if the requested culture is unsupported.</span></span> <span data-ttu-id="985b2-102">Durch die Protokollierung einer `LogLevel.Warning` pro Anforderung können große Protokolldateien mit redundanten Informationen entstehen.</span><span class="sxs-lookup"><span data-stu-id="985b2-102">Logging one `LogLevel.Warning` per request is can make large log files with redundant information.</span></span> <span data-ttu-id="985b2-103">Dieses Verhalten wurde in ASP.NET 3.0 geändert.</span><span class="sxs-lookup"><span data-stu-id="985b2-103">This behavior has been changed in ASP.NET 3.0.</span></span> <span data-ttu-id="985b2-104">Die `RequestLocalizationMiddleware` schreibt ein Protokoll vom Typ `LogLevel.Debug`, wodurch die Größe der Produktionsprotokolle reduziert wird.</span><span class="sxs-lookup"><span data-stu-id="985b2-104">The `RequestLocalizationMiddleware` writes a log of type `LogLevel.Debug`, which reduces the size of production logs.</span></span>