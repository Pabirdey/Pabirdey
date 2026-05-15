using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;

namespace iMonitor_Web.Models
{

    public class BFViewModel
    {
        public BFViewModel()
        {
            Furnaces = new List<GBFTOIBFPRODUCTION>();
        }

        public List<GBFTOIBFPRODUCTION> Furnaces { get; set; }

        public decimal DISPLAY_ACTUAL { get; set; }

        public decimal DISPLAY_REPORTED { get; set; }

        public decimal DISPLAY_BALANCE { get; set; }

        public decimal DISPLAY_ACTUAL_TD { get; set; }

        public decimal DISPLAY_REPORTED_TD { get; set; }
    }



    public class GBFTOIBFPRODUCTION
    {
        #region BASIC DETAILS

        public string FURNACE { get; set; }

        public DateTime TIMESTAMP { get; set; }

        public decimal ACTUAL { get; set; }

        public decimal REPORTED { get; set; }

        public decimal BALANCE { get; set; }

        public decimal ACTUAL_TD { get; set; }

        public decimal REPORTED_TD { get; set; }



        public decimal LD1_TONS { get; set; }

        public decimal LD2_TONS { get; set; }

        public decimal LD3_TONS { get; set; }

        public decimal MRDTP_TONS { get; set; }

        public decimal NOOFTP { get; set; }




        public decimal LD1_TONS_ACTUAL { get; set; }

        public decimal LD2_TONS_ACTUAL { get; set; }

        public decimal LD3_TONS_ACTUAL { get; set; }

        public decimal MRDTP_TONS_ACTUAL { get; set; }



        public decimal DISPLAY_ACTUAL { get; set; }

        public decimal DISPLAY_REPORTED { get; set; }

        public decimal DISPLAY_BALANCE { get; set; }

        public decimal DISPLAY_ACTUAL_TD { get; set; }

        public decimal DISPLAY_REPORTED_TD { get; set; }


    }


}
}
