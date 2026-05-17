 $(".reported").each(function () {

        let id = this.id;

        originalValues[id] = Number($(this).val()) || 0;

    });
