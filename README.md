# LabWork4

using Microsoft.Extensions.Logging;
using System;
using System.Threading.Tasks;

public class LoggingService
{
    private readonly ILogger<LoggingService> _logger;

    public LoggingService(ILogger<LoggingService> logger)
    {
        _logger = logger;
    }

    public async Task<T> ExecuteWithLoggingAsync<T>(Func<Task<T>> func)
    {
        try
        {
            _logger.LogInformation("Начало выполнения операции.");
            var result = await func();
            _logger.LogInformation("Операция успешно завершена.");
            return result;
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Произошла ошибка при выполнении операции.");
            throw;
        }
    }
}
